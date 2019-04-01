# shortest-job-first
Design a scheduler following non-preemptive scheduling approach to schedule the
processes that arrives at different units and having burst time double the arrival time. Scheduler
selects the process with largest burst time from the queue for the execution. Process is not being
preempted until it finishes its service time. Compute the average waiting time and average
turnaround time. What should be the average waiting time if processes are executed according to
Shortest Job First scheduling approach with the same attribute values.





#include<stdio.h>
#include<conio.h>
#include<string.h>
void main()
{
    int bt[20],at[10],n,i,j,temp,st[10],ft[10],wt[10],ta[10];
    int totwt=0,totta=0;
    float awt,ata;
    char pn[10][10],t[10];
    //clrscr();
    
    
    printf("Enter the number of process:  ");
    scanf("%d",&n);
    printf("\n\n\t****************Enter the Name and Arrival time for each process************\n\n");
    for(i=0; i<n; i++)
    {
        printf("Enter process name, arrival time for %d  :   ",i);
        //flushall();
        scanf("%s%d",pn[i],&at[i]);
    }
    for(i=0; i<n; i++)
    {
       bt[i]=2*at[i];
    }
    for(i=0; i<n; i++)
      {
	
        for(j=0; j<n; j++)
        {
            if(bt[i]<bt[j])
            {
                temp=at[i];
                at[i]=at[j];
                at[j]=temp;
                temp=bt[i];
                bt[i]=bt[j];
                bt[j]=temp;
                strcpy(t,pn[i]);
                strcpy(pn[i],pn[j]);
                strcpy(pn[j],t);
            }
        }
      }
    for(i=0; i<n; i++)
    {
    	 if(i==0)
            st[i]=at[i];
        else
            st[i]=ft[i-1];
        wt[i]=st[i]-at[i];
        ft[i]=st[i]+bt[i];
        ta[i]=ft[i]-at[i];
       
        totwt+=wt[i];
        totta+=ta[i];
    }
    awt=(float)totwt/n;
    ata=(float)totta/n;
    printf("\nPname\tarrivaltime\texecutiontime\twaitingtime\ttatime");
    for(i=0; i<n; i++)
        printf("\n%s\t%5d\t\t%5d\t\t%5d\t\t%5d",pn[i],at[i],bt[i],wt[i],ta[i]);
    printf("\n\nAverage waiting time is:%f",awt);
    printf("\n\nAverage turnaroundtime is:%f",ata);
    
    printf("\n\n\t*****calculating Average waiting time and Turnaround time using SJF with same attributes****\n");
    totwt=0;
    totta=0;
        for(i=0; i<n; i++)
      {
	
        for(j=0; j<n; j++)
        {
            if(bt[i]>bt[j])
            {
                temp=at[i];
                at[i]=at[j];
                at[j]=temp;
                temp=bt[i];
                bt[i]=bt[j];
                bt[j]=temp;
                strcpy(t,pn[i]);
                strcpy(pn[i],pn[j]);
                strcpy(pn[j],t);
            }
        }
      }
   
    for(i=0; i<n; i++)
    {
        if(i==0)
            st[i]=at[i];
        else
            st[i]=ft[i-1];
        wt[i]=st[i]-at[i];
        ft[i]=st[i]+bt[i];
        ta[i]=ft[i]-at[i];
        totwt+=wt[i];
        totta+=ta[i];
    }
      awt=(float)totwt/n;
    ata=(float)totta/n;
    printf("\nPname\tarrivaltime\texecutiontime\twaitingtime\ttatime");
    for(i=0; i<n; i++)
        printf("\n%s\t%5d\t\t%5d\t\t%5d\t\t%5d",pn[i],at[i],bt[i],wt[i],ta[i]);
    printf("\n\nAverage waiting time is:%f",awt);
    printf("\n\nAverage turnaroundtime is:%f",ata);
    getch();
}
