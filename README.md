# hello-world
new repository
#include"circularList.h"
#include<iostream>
//Provide the implementation for the CircularList class in this file.

template<class T>
ostream& operator<<(ostream& os, CircularList<T>& ll) {
	Node<T>* X = ll.getLeader();
	if (ll.isEmpty())
	{
		os << "Empty " << endl;
	}
	
	
	else if(X->next  == ll.getLeader())
	{
		os << "[" <<X->data << "]" << endl;
	}
	else
	{
		Node<T>* K = ll.getLeader();
		os << "["; 
		
		while(K->next != ll.getLeader())
		{
			os<<K-> data;
			K = K-> next;
			if(K->next == ll.getLeader())
			{
				os << "]" << endl;
			}
			else
				os << "," ;
			
		}
		
	}
	return os;
}

template<class T>		
CircularList<T>::CircularList(){
    
	this->head = 0;
}

template<class T>
CircularList<T>::CircularList(const CircularList<T>& other) {
	if(other.getLeader() != 0)
	{
		
		this ->head = new Node<T>(*(other.getLeader()));
		
		Node<T>* nodePtr;
		Node<T>* newNode;
		
		nodePtr  =other.getLeader();
		newNode = this->head;
		if(nodePtr->next == this->head)
		{
			newNode  = new Node<T>(*(other.getLeader()));
			this -> head = newNode;
			newNode -> next = this->head;
			
		}
		else
		{
		while(nodePtr->next != other.getLeader())
		{
			newNode -> next=  new Node<T>(*(nodePtr->next));
			newNode = newNode ->next;
			nodePtr = nodePtr ->next;
				
			
		}
		newNode ->next = this -> head;
		}
	}
	else
		this->head =0;

}

template<class T>
CircularList<T>& CircularList<T>::operator=(const CircularList<T>& other) {
	if(this->head != other.getLeader())
	{
		this->head = new Node<T>(*other.getLeader());
		
		Node<T> *newNode;
		Node<T> *nodePtr;
		
		nodePtr = other.getLeader();
		newNode = this->head;
		
		while(nodePtr->next != other.getLeader())
		{
			newNode->next = new Node<T>(*nodePtr->next);
			newNode = newNode -> next;
			nodePtr = nodePtr -> next;
		}
	}
	else
	{
		clear();
		this->head = NULL;
	}
}

template<class T>
CircularList<T>* CircularList<T>::clone() {
	
}

template<class T>
CircularList<T>::~CircularList(){
	Node<T>* nodePtr;
	Node<T>* nextNode;
	
	nodePtr = this->head;
	
	while (nodePtr != NULL)
	{
		nextNode = nodePtr->next;
		delete nodePtr;
		nodePtr = nextNode;
	}
}
	
template<class T>
void CircularList<T>::insert(int index, T data) {
		
	Node<T> *newNode;
	Node<T> *temp1 = new Node<T>(data);
	temp1-> data = data;
	temp1 ->next = this ->head;
	 
	newNode = new Node<T>(data);
	if((index >= 0)&&(index <= size()))
	{
              if(this -> head ==0)
	      {
		      this->head = newNode;
		      newNode-> next = this->head;
	      }
	      else if(index == size()+1)
	      {
		      Node<T> *nodePtr = this->head;
		      int K =0;
		      while(K < index)
		      {
			      nodePtr = nodePtr -> next;
			      K++;
		      }
		      nodePtr-> next = newNode;
	      }
	      else if(index ==1)
	      {
		      temp1-> next = this-> head;
		      this->head = temp1;
	      }
	      else if(index ==0)
	      {
		         temp1-> next = this-> head;
		         this->head = temp1;
	      }
	      else
	      {
		      Node<T>* curr = this->head;
		      for(int i=0;i < index -2;i++)
		      {
			      curr = curr->next;
		      }
		      temp1 -> next = curr->next;
		      curr->next = temp1;
	      }
	}
	
	else
	{
		throw "invalid index";
	}
	
}
	
	
template<class T>
T CircularList<T>::remove(int index){
	 Node<T> *current;
      Node<T> *temp;
      current = this->head;
	
	if (isEmpty())
	{
		throw "empty structure";
	}
	else if((index >size()+1)|| (index < 0))
	{
		throw "invalid index";
	}
	else
	if(index == 0)
	{
		delete current;
	}
	else
	{
      int K =0;
      while(current->next != this->head)
      {
	if(K == index)
	{
             temp = current->next;
	     current->next = current->next->next;
	     delete current->next;
	 }
		K++;	 
  	     		
      }
      }
}
	
template<class T>	
T CircularList<T>::get(int index) const {
	 if (index < 0 || index > size())
	 {
            throw "invalid index";
	 }
	 else if(!this->head)
	 {
		 throw "empty structure";
	 }
	 else
	 {

		Node<T>* current = this->head;
		for (int i = 0; i < index -1; i++)
		 current = current->next;
		 

		return current->data;
	 }
}

template<class T>
bool CircularList<T>::isEmpty() {
	if (this->head == NULL)
		return true;
	else 
		return false;
}

template<class T>
void CircularList<T>::clear() {
	Node<T> *nodePtr;
	Node<T> *nextNode;
	
	nodePtr = this->head;
	
	while(nodePtr->next  != this->head)
	{
		nextNode = nodePtr->next;
		delete nodePtr;
		nodePtr = nextNode;
	}
	delete nodePtr;
	delete nextNode;
}

template<class T>
Node<T>* CircularList<T>::getLeader() const{
	return this->head;
}

template<class T>
ostream& CircularList<T>::print(ostream& os){
	cout << os << endl;
}

template<class T>
int CircularList<T>::size() const{
	if (this->head == NULL)
	{
		return 0;
	}
	
	Node<T> *temp = this->head;
	int counter =0;
	while(temp != NULL)
	{
		counter +=1;
		temp = temp->next;
	}
	delete temp;
	return counter;
}

template <class T>
CircularList<T>& CircularList<T>::operator+(const CircularList<T>& other){
	
}
