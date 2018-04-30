# Classroom-Projects
#include<iostream>
#include<stack>
#include<string>
#include <stdio.h>
#include <string.h>
#include <algorithm>
using namespace std;

//This assignment deals with building an expression tree and evaluating it
//By Tofik Mussa and Kirubel Asfaw
//Submitted to: Dr. Kacem

class BSTNode {
public:
	char el;
	BSTNode *left;
	BSTNode *right;

	BSTNode(char elm) {
		el = elm;
	}
};

bool checkParenthesis(string stg) { // checks for matching parenthesis

	char * charray = new char[stg.length() + 1];
	strcpy_s(charray, stg.length() + 1, stg.c_str());

	stack<char>s1;
	stack<char>s2;

	for (int unsigned i = 0; i < stg.length(); i++) {
		if (charray[i] = '(') {
			s1.push(charray[i]);
		}

		if (charray[i] = ')') {
			s2.push(charray[i]);
		}
	}

	if (s1.size() == s2.size())
		return true;
	return false;
}

string infixToPostfixConverter(string stg) { //function to change postfix to infix
	stack<char> s1;
	string postfix = " ";
	char *stginfix = new char[stg.length() + 1];
	strcpy_s(stginfix, stg.length() + 1, stg.c_str());

	if (checkParenthesis(stg) == false) { //Exit the function if non-matching parenthesis 
		cout << "Matching parenthesis not found " << "\n";
		return 0;
	}

	for (int unsigned i = 0; i < stg.length(); i++) {

		if (stginfix[i] == '*' || stginfix[i] == '/' || stginfix[i] == '+' || stginfix[i] == '-') {
			s1.push(stginfix[i]);
		}
		else if (stginfix[i] >= '0' && stginfix[i] <= '9') {
			postfix += stginfix[i];
		} 
		else if (stginfix[i] == '(') {
			s1.push(stginfix[i]);
		}
		else if (stginfix[i] == ')') {
			while (!s1.empty() && s1.top() != '(') {
				postfix += s1.top();
				s1.pop();
			}
		}

	}
	while (!s1.empty()) {
		postfix += s1.top();
		s1.pop();
	}
	return postfix;
}

BSTNode* formTree(string express) {//constructing the tree

	stack<BSTNode*>BSTstack;
	BSTNode *node, *node1, *node2;
	char *charray = new char[express.length() + 1];
	strcpy_s(charray, express.length() + 1, express.c_str());

	for (int unsigned i = 0; i < express.length(); i++) {

		if (charray[i] >= '0'&& charray[i] <= '9') {
			node = new BSTNode(charray[i]);
			BSTstack.push(node);
		} 
		else if (charray[i] == '*' || charray[i] == '/' || charray[i] == '+' || charray[i] == '-')
		{
			node = new BSTNode(charray[i]);

			node1 = BSTstack.top();
			BSTstack.pop();

			node2 = BSTstack.top();
			BSTstack.pop();

			node->right = node1;
			node->left = node2;

			BSTstack.push(node);
		}
	}
	return BSTstack.top();
}

void inorder(BSTNode *bst) {//traversing the tree
	if (bst) {
		inorder(bst->left);
		cout << bst->el;
		inorder(bst->right);
	}
}

int evaluateTree(BSTNode *bst) {//evaluating the tree
	if (!bst) {
		return 0;
	}

	if (!bst->left && !bst->right) {
		return bst->el - '0'; //gives us difference in ASCII value which is the desired result
	}

	int leftValue = evaluateTree(bst->left);
	int rightValue = evaluateTree(bst->right);

	if (bst->el == '+') {
		return leftValue + rightValue;
	}
	if (bst->el == '-') {
		return leftValue - rightValue;
	}
	if (bst->el == '*') {
		return leftValue * rightValue;
	}
	if (bst->el == '/') {
		return leftValue / rightValue;
	}
}


int main()
{
	string expression = infixToPostfixConverter("(((9+1)/2)*3)-4");
	BSTNode * bt = formTree(expression);

	cout << "Inorder traversal of the tree gives " << "\n";
	inorder(bt);
	cout << "\n";

	cout << "The computed answer is " << "\n";
	cout << evaluateTree(bt);
	cout << "\n";

	system("pause");
	return 0;
}
