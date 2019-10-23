#include<iostream>
#include<string>
using namespace std;
void division(int temp[],int gen[],int n,int r)
{
 for(int i=0;i<n;i++)
 {
     if (gen[0]==temp[i])
     {
         for(int j=0,k=i;j<r+1;j++,k++)
             if(!(temp[k]^gen[j]))
                 temp[k]=0;
             else
                 temp[k]=1;
     }
 }
}
int main()
{int n,r,message[50],gen[50],temp[50];
 string data,generator;
 cout<<"Enter data: ";
 cin>>data;
 cout<<"Generating polynomial: ";
 cin>>generator;
 n=data.length();
 r=generator.length();
 for(int i=0;i<n;i++)
     message[i]=data[i]-'0';
 for(int i=0;i<r;i++)
     gen[i]=generator[i]-'0';
 r--;
 for(int i=0;i<r;i++)
     message[n+i] = 0;
 cout<<"Modified data is: "<<endl;
 for(int i=0;i<n+r;i++) {
     temp[i] = message[i];
     cout<<message[i];
 }
 cout<<endl;
 division(temp,gen,n,r);
 cout<<"CRC checksum is : ";
 for(int i=0;i<r;i++)
 {
     cout<<temp[n+i]<<" ";
     message[n+i] = temp[n+i];
 }
 cout<<endl<<"Final codeword transmitted is : ";
 for(int i=0;i<n+r;i++)
     cout<<message[i]<<" ";
 int flag;
 cout<<endl<<"Test error detection 0<yes> 1<no>"<<endl;
 cin>>flag;
 if(flag) {
     cout<<"CRC checksum is : ";
     for(int i=0;i<n+r;i++)
          cout<<'0';
     cout<<endl<<"No error detected"<<endl;
 }
 else{ 
     int pos;
     cout<<"Enter the position where error is to be inserted :";
     cin>>pos;
     for(int i=0;i<n+r;i++) {
        if(i==pos-1) {
          if(message[i]==0)
            temp[i]=1;
          else
            temp[i]=0;
          }
        else
         temp[i] = message[i];
     }
     cout<<"Erroneous data : ";
     for(int i=0;i<n+r;i++)
       cout<<temp[i];
     cout<<endl;
     division(temp,gen,n,r);
     cout<<"CRC checksum is : ";
     for(int i=0;i<r;i++)
     {
        cout<<temp[n+i]<<" ";
         
     }
     cout<<endl<<"Error detected"<<endl;
 }
 return 0;
}