#include<stdio.h>
#include<string.h>
#include<stdlib.h>
#define tpass 1234
typedef struct student
{
   char USN[12];
   char name[20];
   char branch[5];
   int sem;
   char pass[10];
   char status;
   int score;
}student;

typedef struct teacher
{
   char Question[100];
   char answer;
   char storedanswer;
}teacher;

void create(int teacherpass)
{
   student s;
   FILE *fp;
   int n,i;
   if(teacherpass!=tpass)
   {
      printf("\n\tINCORRECT PASSWORD");
      return;
   }
   if(teacherpass==tpass)
   {
      printf("\n\tEnter number of students:");
      scanf("%d",&n);
      fp=fopen("sturec.txt","w");
      for(i=0;i<n;i++)
      {
         printf("\n\tEnter the Name: ");
           scanf(" %[^\n]*c",s.name);
         printf("\tEnter the USN:");
         scanf("%s",s.USN);
         printf("\tEnter the Branch:");
         scanf("%s",s.branch);
         printf("\tEnter the Sem:");
         scanf("%d",&s.sem);
         printf("\tEnter the unique password:");
         scanf("%s",s.pass);
         fwrite(&s,sizeof(student),1,fp);
      }
   }
   fclose(fp);
}

void display(int teacherpass)
{
   student s1;
   FILE *fp;
   if(teacherpass!=tpass)
   {
      printf("\n\tINCORRECT PASSWORD");
      return;
   }
   if(tpass==teacherpass)
   {
      fp=fopen("sturec.txt","r");
      if(fp==NULL)
      {
         printf("\n\tNO RECORDS PRESENT");
         return;
      }
      printf("\n\t---------------------------------------------------------------------------------------");
      printf("\n\t\t\t\t************STUDENT RECORDS************\n");
      printf("\t---------------------------------------------------------------------------------------\n\n");
      while(fread(&s1,sizeof(student),1,fp))
      {
         printf("\n");
         printf("\t\t\tUSN : %s\t\t\tNAME : %s\n",s1.USN,s1.name);
         printf("\t---------------------------------------------------------------------------------------");
      }
   }
   fclose(fp);
}

void questionpaper(student s1)
{
   FILE *fp;
   char a1,a2,a3,a4,a5,a6,a7,a8,a9,a10;
   int count=0;
   char res;
   printf("\n\t\t~~~~~~~~~~~~~~~~~~TEST~~~~~~~~~~~~~~~~~\n");
   char q1[500]={"\n\t1.Which of the following language is the predecessor to C Programming Language?\n\ta) A\n\tb) B\n\tc) BCPL\n\td) C++"};
   printf("%s",q1);
   printf("\n\tEnter your answer: ");
   scanf(" %c",&a1);
   if(a1=='c')
   {
      count++;
   }
   char q2[500]={"\n\t2.C programming language was developed by:\n\ta) Dennis Ritchie\n\tb) Ken Thompson\n\tc) Bill Gates\n\td) Peter Norton"};
   printf("%s",q2);
   printf("\n\tEnter your answer: ");
   scanf(" %c",&a2);
   if(a2=='a')
   {
      count++;
   }
   char q3[500]={"\n\t3. C was developed in the year ___\n\tta) 1970\n\tb) 1972\n\tc) 1976\n\td) 1980"};
   printf("%s",q3);
   printf("\n\tEnter your answer: ");
   scanf(" %c",&a3);
   if(a3=='b')
   {
      count++;
   }
   char q4[500]={"\n\t4. C is a ___ language\n\ta) High Level\n\tb) Low Level\n\tc) Middle Level\n\td) Machine Level"};
   printf("%s",q4);
   printf("\n\tEnter your answer: ");
   scanf(" %c",&a4);
   if(a4=='c')
   {
      count++;
   }
   char q5[500]={"\n\t5. C language is available for which of the following Operating Systems?\n\ta) DOS\n\tb) Windows\n\tc) Unix\n\td) All of these"};
   printf("%s",q5);
   printf("\n\tEnter your answer: ");
   scanf(" %c",&a5);
   if(a5=='d')
   {
      count++;
   }
   char q6[500]={"\n\t6. Which of the following symbol is used to denote a pre-processor statement?\n\ta) !\n\tb) #\n\tc) ~\n\td) \n\t;"};
   printf("%s",q6);
   printf("\n\tEnter your answer: ");
   scanf(" %c",&a6);
   if(a6=='b')
   {
      count++;
   }
   char q7[500]={"\n\t7. Which of the following is a Scalar Data type\n\ta) Float\n\tb) Union\n\tc) Array\n\td) Pointer"};
   printf("%s",q7);
   printf("\n\tEnter your answer: ");
   scanf(" %c",&a7);
   if(a7=='a')
   {
      count++;
   }
  
   char q8[500]={"\n\t8. Which of the following are tokens in C?\n\ta) Keywords\n\tb) Variables\n\tc) Constants\n\td) All of the above"};
   printf("%s",q8);
   printf("\n\tEnter your answer: ");
   scanf(" %c",&a8);
   if(a8=='d')
   {
      count++;
   }
   char q9[500]={"\n\t9. What is the valid range of numbers for int type of data?\n\ta) 0 to 256\n\tb) -32768 to +32767\n\tc) -65536 to +65536\n\td) No specific range"};
   printf("%s",q9);
   printf("\n\tEnter your answer: ");
   scanf(" %c",&a9);
   if(a9=='b')
   {
      count++;
   }
   char q10[500]={"\n\t10. The maximum length of a variable in C is ___\n\ta) 8\n\tb) 16\n\tc) 32\n\td) 64"};
   printf("%s",q10);
   printf("\n\tEnter your answer: ");
   scanf(" %c",&a10);
   if(a10=='d')
   {
      count++;
   }
   printf("\n");
   printf("\n\tYou have %d correct answers out of 10",count);
   if(count>4)
   {
      printf("\n\tTest status : PASS");
      res='P';
   }
   else
   {
      printf("\n\tTest status : FAIL");
      res='F';
   }
   fp=fopen("report.txt","a");
   s1.score=count;
   s1.status=res;
   fwrite(&s1,sizeof(student),1,fp);
   fclose(fp);
}

void studententry()
{
   student s1;
   char spass[20];
   int found=0;
   FILE *fp;
   fp=fopen("sturec.txt","r");
   if(fp==NULL)
   {
      printf("\n\tENTRIES HAVE NOT BEEN MADE");
      return;
   }
   printf("\n\tEnter your password: ");
   scanf("%s",spass);
   while(fread(&s1,sizeof(student),1,fp))
   {
      if((strcmp(s1.pass,spass)==0))
      {
          printf("\n\t--STUDENT DETAILS--\n\n");
          printf("\tUSN: %s\n\tNAME: %s\n\tBRANCH: %s\n\tSEM: %d\n",s1.USN,s1.name,s1.branch,s1.sem);
          found=1;
          questionpaper(s1);
          return;
      }
   }
       if(!found)
       {
         printf("\n\tINCORRECT PASSWORD");
       }
   fclose(fp);
}

void displayall(int teacherpass)
{
   student s1;
   FILE *fp;
   if(teacherpass!=tpass)
   {
      printf("\n\tINCORRECT PASSWORD");
      return;
   }
   if(tpass==teacherpass)
   {
       fp=fopen("report.txt","r");
       if(fp==NULL)
       {
          printf("\n\tNO RECORDS");
          return;
       }
       printf("\t--------------------------------------------------------");
       printf("\n\t\t\t*****STUDENT RECORDS*****\n");
       printf("\t--------------------------------------------------------\n");
       while(fread(&s1,sizeof(student),1,fp))
       {
          printf("\t----------------------------\n");
          printf("\tUSN\t: %s\n\tNAME\t: %s\n\tBRANCH\t: %s\n\tSEM\t: %d\n\tSCORE\t: %d\n\tSTATUS\t: %c\n",s1.USN,s1.name,s1.branch,s1.sem,s1.score,s1.status);
          printf("\t----------------------------\n");
          printf("\n");
       }
   }
   fclose(fp);
}

void createqp(int teacherpass)
{
   teacher t;
   FILE *fp;
   int n,i;
   if(teacherpass!=tpass)
   {
      printf("\n\tINCORRECT PASSWORD");
      return;
   }
   if(teacherpass==tpass)
   {
    
      fp=fopen("quesp.txt","w");
      for(i=0;i<10;i++)
      {
         printf("\n\tEnter the Question: ");
         scanf(" %[^\n]*c",t.Question);
         printf("\n\tEnter the Answer:");
         scanf(" %c",&t.answer);
         t.storedanswer=t.answer;
         fwrite(&t,sizeof(teacher),1,fp);
      }
   }
   fclose(fp);
}

void newtest()
{
   teacher t1;
   student s1;
   char spass[20];
   int found=0;
   FILE *fp;
   FILE *lp;
   char ans;
   char res;
   int count=0;
   fp=fopen("sturec.txt","r");
   printf("\n\tEnter your password: ");
   scanf("%s",spass);
   while(fread(&s1,sizeof(student),1,fp))
   {
      if((strcmp(s1.pass,spass)==0))
      {
          printf("\n\tSTUDENT DETAILS:\n");
          printf("\tUSN: %s\n\tNAME: %s\n\tBRANCH: %s\n\tSEM: %d\n",s1.USN,s1.name,s1.branch,s1.sem);
          printf("\n\tStart the test and choose among a,b,c,d\n");
          found=1;
          lp=fopen("quesp.txt","r");
          while(fread(&t1,sizeof(teacher),1,lp))
          {
            printf("\n\t%s",t1.Question);
            printf("\n\tEnter your answer:  ");
            scanf(" %c",&ans);
            if(ans==t1.storedanswer)
            {
               count++;
            }
          }
             printf("\n\tYour score is %d",count);
             if(count>4)
             {
                printf("\n\tTest status : PASS");
                res='P';
             }
             else
             {
                printf("\n\tTest status : FAIL");
                res='F';
             }
             fp=fopen("newreport.txt","a");
             s1.score=count;
             s1.status=res;
             fwrite(&s1,sizeof(student),1,fp);
             fclose(fp);
             return;
      }
   }
         if(!found)
         {
             printf("\n\tINCORRECT PASSWORD");
             return;
         }
          fclose(fp);
          fclose(lp);
}

void displaynew(int teacherpass)
{
   student s1;
   FILE *fp;
   if(teacherpass!=tpass)
   {
      printf("\n\tINCORRECT PASSWORD");
      return;
   }
   if(tpass==teacherpass)
   {
       fp=fopen("newreport.txt","r");
       if(fp==NULL)
       {
          printf("\n\tNO NEW RECORDS MADE");
          return;
       }
       printf("\n\t\t\t*****STUDENT RECORDS*****\n\n");
       while(fread(&s1,sizeof(student),1,fp))
       {
          printf("\tUSN: %s \n\tNAME: %s\n\tSEM: %d\n\tSCORE: %d\n\tSTATUS: %c\n",s1.USN,s1.name,s1.sem,s1.score,s1.status);
          printf("\n");
       }
   }
   fclose(fp);
}

int main()
{
   int ch;
   int teacherpass;
   printf("\n\t\t\t\t\t\t\t\t ******|ONLINE EXAM INTERFACE|******");
   printf("\n\n\n\tCHOICE 1-5 ARE ONLY FOR TEACHER\n");
   printf("\tSTUDENTS TO ENTER ONLY OPTION 6 OR 7\n");
   while(1)
   {
      printf("\n");
      printf("\tMENU");
      printf("\n\t~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~");
      printf("\n\t1.CREATE\n\t2.DISPLAY RECORDS");
      printf("\n\t3.DISPLAY ALL REPORTS");
      printf("\n\t4.CREATE NEW PAPER");
      printf("\n\t5.DISPLAY NEW REPORT");
      printf("\n\t6.TEST");
      printf("\n\t7.NEW TEST");
      printf("\n\t8.EXIT");
      printf("\n\t~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~");
      printf("\n\tEnter your choice:");
      scanf("%d",&ch);
      if(ch>8||ch<1)
      {
         printf("Wrong Choice");
         return;
      }
      switch(ch)
      {
         case 1:printf("\n\tEnter the teacher password : ");
                scanf("%d",&teacherpass);
                create(teacherpass);
                break;
         case 2:printf("\n\tEnter the teacher password : ");
                scanf("%d",&teacherpass);
                display(teacherpass);
                break;
         case 3:printf("\n\tEnter the teacher password : ");
                scanf("%d",&teacherpass);
                displayall(teacherpass);
                break;
         case 4:printf("\n\tEnter the teacher password : ");
                scanf("%d",&teacherpass);
                createqp(teacherpass);
                break;
         case 5:printf("\n\tEnter the teacher password : ");
                scanf("%d",&teacherpass);
                displaynew(teacherpass);
                break;
         case 6:studententry();
                break;
         case 7:newtest();
                break;
         case 8:exit(0);
      }
   }
}