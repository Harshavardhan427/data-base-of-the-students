# data-base-of-the-students
#include<iostream>
#include<cstdio>
#include<cstring>
#include<cstdlib>
#include<conio.h>
#include<iomanip>
using namespace std;
int main()
{
	FILE *fp,*ft;
	char another,choice;
		
   struct student
   {
   	char first_name [50],last_name[50];
   	char course[100];
   	int section;
   };
   
   struct student e;
   char xfirst_name[50],xlast_name[50];
   long int recsize;
   fp=fopen("users.txt","rb+");
   if(fp==NULL)
   {
   	fp=fopen("users.txt","wb+");
   	if(fp=NULL)
   	{
   		puts("cannnot open file");
   		return 0;
	   }
   }
   recsize = sizeof (e);
   while(1)
   {
   	system("cls");
   	cout<<"\t\t======STUDENT DATABASE MANAGEMENT======";
   	cout<<"\n\n";
   	cout<<"\n\t\t\t 1.Add record";
   	cout<<"\n\t\t\t 2.List record";
   	cout<<"\n\t\t\t 3.Modify record";
   	cout<<"\n\t\t\t 4.Delete record";
   	cout<<"\n\t\t\t 5. Exit program";
   	cout<<"\n\n";
   	cout<<"\t\t\t select your choice:=> ";
   	fflush(stdin);
   	choice = getche();
   	switch(choice)
   	{
   		case '1':
   			fseek(fp,0,SEEK_END);
   			another ='Y';
   			while (another=='y' || another =='Y')
   			{
   				system("cls");
				cout<<"enter the first name : ";
				cin>>e.first_name;
				cout<<"enter the last name : ";
				cin>>e.last_name;
				cout<<"enter the  section : ";
				cin>>e.section;
				fwrite(&e,recsize,1,fp);
				cout<<"\n Add another record (Y/N)";
				fflush(stdin);
				another=getchar();			   
				   }
				   break;
		case'2':
			system("cls");
			rewind(fp);
			cout<<"===view the recordsin the data base===";
			cout<<"\n";
			while(fread(&e,recsize,1,fp)==1)
			{
				cout<<"\n";
				cout<<"\n";
				cout<<e.first_name;
				cout<<setw(10);
				cout<<e.last_name;
				cout<<"\n";
				cout<<e.course<<setw(8)<<e.section;
			}
			cout<<"\n";
			system("pause");
			break;
			
			case '3':
				system("cls");
				another='Y';
				while(another=='Y'||another=='Y')
				{
					cout<<"\n enter the last name of the student : ";
					cin>>xlast_name;
					rewind(fp);
					while (fread(&e,recsize,1,fp)==1)
					{
						if(strcmp(e.last_name,xlast_name)==0)
						{
						cout<<"enter the new first name : ";
				        cin>>e.first_name;
				        cout<<"enter the new last name : ";
				        cin>>e.last_name;
			            cout<<"enter the new section : ";
				        cin>>e.section;
				        cout <<"enter the new course";
				        cin>>e.course;
				        fseek(fp,-recsize,SEEK_CUR);
				        fwrite(&e,recsize,1,fp);
				        break;
						}
					else
					cout<<"record not found";
					}
				cout<<"\n Modify the Another record (Y/N)";
				fflush(stdin);
				another='Y';
				}
				break;
			case '4':
				system("cls");
				another ='Y';
				while(another=='Y'||another=='Y')
				{
					cout<<"\n enter the last name of the student to delete : ";
					cin>>xlast_name;
					ft=fopen("temp.dat","wb");
					rewind(fp);
					while(fread(&e,recsize,1,fp)==1)
					if(strcmp(e.last_name,xlast_name)!=0)
					{
						fwrite(&e,recsize,1,ft);
					}
					fclose(fp);
					fclose(ft);
					remove("users.txt");
					rename("temp.dat","users.txt");
					fp=fopen("users.txt","rb+");
					cout<<"\n delete another record(Y/N)";
					fflush(stdin);
					another=getchar();
				}
				break;
			case '5':
				fclose(fp);
				cout<<"\n\n";
				cout<<"\t\t THANK YOU FOR USING THIS SOFTWARE ";
				cout<<"\t\t";
				exit(0);
	   }
   		
   	
   }
   system("pause");
   return 0;
   
}
