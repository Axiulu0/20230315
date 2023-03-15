#include <iostream>
#include <string>

#define MAXDATA 100
typedef unsigned int ElementType;
typedef struct node {
	ElementType data;
	struct node * next;
} SLinkNode;
typedef SLinkNode* SLinkList;


int CreateList(SLinkList & L){
	std::cout << "input data:\n";
	L = (SLinkList)malloc(sizeof(SLinkNode));
	L->next = NULL;
	SLinkNode* aNode, *aTail=L;
	ElementType aData;

	int counter=0;
	std::cin >> aData;
	while(counter<MAXDATA && aData != -1){
		aNode = (SLinkList)malloc(sizeof(SLinkNode));
		aNode->data = aData;
		aNode->next = NULL;
		aTail->next = aNode;
		aTail = aNode;
		counter ++;
		std::cin >> aData;
	}
	return 0;
}

int DispList(const SLinkList & L){
	SLinkNode* aNode = L->next;
	while(aNode != NULL){
		std::cout << aNode->data << "  ";
		aNode = aNode->next;
	}
	std::cout << std::endl;	
	return 0;
}

int DestroyList(SLinkList & L){
	SLinkNode* aNodePre =L, *aNode = L->next;
	/**************
	while( aNode != NULL ){
		free(aNodePre);
		aNodePre = aNode;
		aNode = aNode->next;
	}
	free(aNodePre);
	//**************/

	if( L != NULL ){
		aNode = L->next;
		DestroyList(aNode);
		free(L);
	}
	return 0;
}

int SplitList(
	SLinkList & aList, SLinkList & bList, 
	SLinkList & cList, const ElementType & aBase){

	bList = (SLinkList)malloc(sizeof(SLinkNode));
	cList = (SLinkList)malloc(sizeof(SLinkNode));
	bList->next = NULL; cList->next = NULL;
	SLinkNode* aNode=aList->next, *bTail= bList, *cTail = cList;


	while(aNode != NULL){
		if(aNode->data < aBase){
			bTail->next = aNode;
			bTail = aNode;
		} else {
			cTail->next = aNode;
			cTail = aNode;
		}
		aNode = aNode->next;
	}
	bTail->next = NULL; cTail->next = NULL;
	aList->next = NULL;
	return 0;
}

int main(){
	SLinkList aList, bList, cList;
	CreateList(aList);

	DispList(aList);

	ElementType aBase;
	std::cout << "input base number:";
	std::cin >> aBase;

	SplitList( aList, bList, cList, aBase );

	std::cout << "aList:\n";
	DispList(aList);
	std::cout << "bList:\n";
	DispList(bList);
	std::cout << "cList:\n";
	DispList(cList);

	DestroyList(aList);DestroyList(bList);DestroyList(cList);
	return 0;
}
