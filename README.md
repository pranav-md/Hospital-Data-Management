# Hospital-Data-Management
My first project
#include<fstream.h>
#include<math.h>
#include<conio.h>
#include <graphics.h>
#include<dos.h>
#include<process.h>
#include<string.h>
#include<stdio.h>
char*month(int);
char*daywk(int);
class patient
{
 int age,numadmt,adflg;
 long int phoneno,opnum;
 char name[20],gender[5],address[10],bldgp[5];

public:
void display(char,int,int,int,int);
int numvis;
 class docndept
 {
 char department[10],doctr[10];
 int date,month,year,day;
 public:
 void gtdta(int d8,int mon,int yr,int dy)
 { cout<<"\t\tENTER DEPARTMENT:";
 gets(department);
 cout<<"\t\tENTER THE DOCTOR TO CONSULT:";
 gets(doctr);
 date=d8;
 month=mon;
 year=yr;
 day=dy;
 }
 char*rdept()
 {return department;}
 char*rdoc()
 {return doctr;}
 int rdate()
 {return date;}
  int rmonth()
 {return month;}
  int ryear()
 {return year;}
  int rday()
 {return day;}
 }pat[100];
 class ward
 {
 int date,month,year,nmdys,rmno;
 char prblm[15],wrd;
 public:
 void admt(int d,int m,char prob[],int rno,char wd)
 { date=d;
   month=m;
   strcpy(prblm,prob);
   rmno=rno;
   wrd=wd;
 }
 void dcharge(int,int);
 int rdate()
 {return date;}
  int rmonth()
 {return month;}
  int ryear()
 {return year;}
 char*rprob()
 {return prblm;}
 int rrmno()
 {return rmno;}
  int rdys()
 {return nmdys;}
 char rwrd()
 {return wrd;}
 }
 wdpat[50];
 patient()
 {}
 int wrdtls();
 patient(int n)
 {
   opnum=n;
   numvis=0;
   numadmt=0;
   adflg=0;
 }
 int wrdadmtf(char p[],int date,int month,int ro,char w)
 {
  if(adflg==1)
  return 0;
  wdpat[numadmt].admt(date,month,p,ro,w);
  adflg=1;
  return 1;
 }
 void dc(int date,int month)
 {
  adflg=0;
  wdpat[numadmt].dcharge(date,month);
  ++numadmt;
 }
 long int opnumr()
{
   return opnum;
}
 void putdata(char dt,int date=0,int month=0,int year=0,int day=0)
{

 cout<<"\n     ENTER NAME:";
 gets(name);
 cout<<"\n     ENTER AGE:";
 cin>>age;
 cout<<"\n     ENTER GENDER:";
 gets(gender);
 cout<<"\n     ENTER ADDRESS:";
 gets(address);
 cout<<"\n     ENTER BLOOD GROUP:";
 gets(bldgp);
 cout<<"\n     ENTER PHONE NO.:";
 cin>>phoneno;
 if(dt=='y')
 {
 pat[numvis].gtdta(date,month,year,day);
 ++numvis;
 }
}



char*raddrss()
{
 return address;
}

char*rname()
{
return name;
}
char*rbldgp()
{
return bldgp;
}
long int rphoneno()
{
return phoneno;
}
};
void patient::display(char dt,int date,int month,int year,int day)
 {
		 cleardevice();
		 cout<<"            |"<<"\n\t    |\n\t"<<"NAME|    "<<name;
		 cout<<"\n--------------------------------------------------------------------------------";
		 cout<<"            |"<<"\n\t    |\n    "<<"OPNUMBER|   "<<opnum;
		 cout<<"\n--------------------------------------------------------------------------------";
		 cout<<"            |"<<"\n\t    |\n     "<<"ADDRESS|    "<<address;
		 cout<<"\n--------------------------------------------------------------------------------";
		 cout<<"            |"<<"\n\t    |\n      "<<"GENDER|    "<<gender;
		 cout<<"\n--------------------------------------------------------------------------------";
		 cout<<"            |"<<"\n\t    |\n"<<"PHONE NUMBER|    "<<phoneno;
		 cout<<"\n--------------------------------------------------------------------------------";
		 cout<<"            |"<<"\n\t    |\n"<<" BLOOD GROUP|    "<<bldgp;
		 cout<<"\n--------------------------------------------------------------------------------";

		 if(dt=='y')
		 {
		 pat[numvis].gtdta(date,month,year,day);
		 ++numvis;
		 }
		 if(dt=='m')
		 {
		 cout<<"\t\tWANT MORE DETAILS??(Y\\N)-";
		 dt=getch();
		  if(dt=='y'||dt=='Y')
		  {
		   cleardevice();
		   cout<<"\n\n\n\n\t1.DOCTOR-APPOINTMENT DETAIL\n\n\n\t2.WARD DETAILS\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n";
		   dt=getch();
		   if(dt==49)
		   {
		   cleardevice();
		   cout<<"\n\n\n\n\n\n\n\n\n\n\n\n";
		    cout<<"\n\tDOCTORS CONSULTED  -------------  DATE"<<"\n--------------------------------------------------------------------------------\n";
		    for(int i=0;i<numvis;++i)
		    cout<<"\n\t"<<i+1<<". DR."<<pat[i].rdoc()<<"("<<pat[i].rdept()<<")"<<" ------------- {"<<pat[i].rdate()<<"."<<::month(pat[i].rmonth())<<"."<<pat[i].ryear()<<" ("<<daywk(day)<<")}";
		   cout<<"\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n";
		 }
		 else
		 if(dt==50)
		 {
		 cleardevice();
		 wrdtls();
		 }
		 }
 }}
void patient::ward::dcharge(int d,int m)
 {
   if(m==month)
   nmdys=d-date;
   else
   if(m>month)
   for(int i=1;i<12;++i)
    if(month==fabs(m-i))
    { nmdys=(i-1)*30+30-date+d;
     break;
    }
   else
   if(month>m)
   {
    nmdys=(12-month+m-1)*30+d;
   }

 }
int patient::wrdtls()
 {
   if(!numadmt)
   {cout<<"\t"<<name<<" DID NOT ADMITTED IN THIS HOSPITAL EVER!!!";
   cout<<"\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n";
   return 0;
   }
   cout<<"\n\t  ROOMNO    DATE          NO.OF DAYS    PROBLEM"<<"\n--------------------------------------------------------------------------------\n";
   for(int i=0;i<numadmt;++i)
   cout<<"\n\t"<<i+1<<". "<<wdpat[i].rwrd()<<"-"<<wdpat[i].rrmno()<<"     "<<wdpat[i].rdate()<<"."<<::month(wdpat[i].rmonth())<<"."<<wdpat[i].ryear()<<"        "<<wdpat[i].rdys()<<"        "<<wdpat[i].rprob();
   cout<<"\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n";
   return 0;
 }

void wrdadmtf(char,int,int,int,char) ;
void pmd(int,int);
long int ename(char);
void ext();
char*month(int);
char*daywk(int);
void admitfun(int);
int ward(char,long int);
long int wsearch(long int ) ;
void main()
{
 clrscr();
char star[10]=" ";
int chi;
long psn=0;
int c=0,i=0;
while(1)
{
 textcolor(BLUE);
 cprintf("ENTER PASSWORD");
 cout<<star;
 chi=getch()-48;
 sound(1000);
 delay(100);
 nosound();
 clrscr();
 if(chi==-35)
 {
  if(psn==1234567)
  break;
  else
  textcolor(RED+BLINK);
  cprintf("TRY AGAIN!!!");
  cout<<psn;
  psn=0;
  chi=0;
  i=0;
  strcpy(star," ");
  getch();
  clrscr();
 }
 else
 if(chi==-40)
 {psn/=10;
  star[i]='\0';
  --i;
 }
 else
 {psn*=10;
 strcat(star,"*");
 psn+=chi;
 ++i;
 }
 }

int gdriver = EGA, gmode = EGAHI,x=200;
fstream file,kfile;
initgraph(&gdriver, &gmode, "c:\\tc\\bgi");
//cleardevice();
//setbkcolor(GREEN);
  setcolor(RED);
   line(x,x,1.7*x,x);
   line(x,x,x,0.75*x);
   line(1.7*x,x,1.7*x,.75*x);
   line(1.35*x,0.7*x,1.35*x,0.5*x);
   line(0.85*x,0.2*x,1.25*x,0.2*x);
   line(1.85*x,0.2*x,1.45*x,0.2*x);
  setcolor(WHITE);

settextstyle(SANS_SERIF_FONT, HORIZ_DIR,1);
   outtextxy(230,240,"WELCOME");
   outtextxy(230,250,"-------");
   delay(2000);
   for(int ik=0;ik<getmaxx();++ik)
   {
   outtextxy(525,310,"LOADING...");
   line(ik,getmaxy()-5,ik,getmaxy());
    delay(10);
   }
   for(ik=0;ik<getmaxy();++ik)
   {
   line(0,getmaxy()-ik,getmaxx(),getmaxy()-ik);
   line(0,ik,getmaxx(),ik);
   delay(1);
   }
   cleardevice();
   setcolor(DARKGRAY);
  pmd(30,1);
  settextstyle(SMALL_FONT, HORIZ_DIR,4);
  setbkcolor(WHITE);
outtextxy(325,50,"TM");
outtextxy(1,330," copyright (C) PMD CORPORATION");
settextstyle(SANS_SERIF_FONT, HORIZ_DIR, 1);
outtextxy(325,260,"SOFTWARES PRESENTZZ..");
delay(3000);
cleardevice();
settextstyle(DEFAULT_FONT, HORIZ_DIR, 2);
outtextxy(250,300,"In ASSO With..");

getch();
cleardevice();
//struct dosdate_t d;
//_dos_getdate(&d);
int ch,cho,wp;
int date,mon;
int day,year;
long int opnm=0;
char dflag='n',name[20];
if(!file)
cout<<"cannot open file!!";
_setcursortype(_NORMALCURSOR);
setcolor(RED);
setbkcolor(LIGHTGREEN);
settextstyle(GOTHIC_FONT, HORIZ_DIR, 4);
outtextxy(200,230," pea");
settextstyle(SMALL_FONT, HORIZ_DIR, 10);
outtextxy(250,270," SOFTWARES...");
settextstyle(SMALL_FONT, HORIZ_DIR, 4);
outtextxy(275,25,"TM");
outtextxy(1,330," pea(C) IS THE COPYRIGHT OF PEA CORPORATION");
settextstyle(SANS_SERIF_FONT, HORIZ_DIR, 1);
//pmd(30,1);
delay(3000);
cleardevice();
setbkcolor(LIGHTRED);
settextstyle(SANS_SERIF_FONT, HORIZ_DIR, 1);
outtextxy(150,150,"PROJECT ON HOSPITAL DATA MANAGEMENT");
delay(3000);
 sound(10000);
 delay(100);
 nosound();
 cleardevice();
cout<<"\n\n\tENTER TODAY'S:";
cout<<"\n\n\t\tDATE ";
cin>>date;
cout<<"\n\n\t\tDAY  ";
cin>>day;
cout<<"\n\n\t\tMONTH  ";
cin>>mon;
cout<<"\n\n\t\tYEAR  ";
cin>>year;
do
{
clrscr();
cleardevice();
opnm=0;
setcolor(BLINK+BLUE);
   for(ik=0;ik<getmaxy();++ik)
   {
   line(0,getmaxy()-ik,getmaxx(),getmaxy()-ik);
   line(0,ik,getmaxx(),ik);
   delay(1);
   }
    cleardevice();
setbkcolor(BLUE);
setcolor(RED);
	pmd(5,1);
	textcolor(YELLOW);
	cout<<"\n\n\n\t\t\tPMD MEDICAL TRUST HOSPITAL";
	cout<<"\n\t\t\t--------------------------"<<"\n\n\t\t\tMAIN MENU";
	cout<<"\n\n\t1.RECEPTIONIST";
	cout<<"\n\n\t2.WARD MANAGER";
	cout<<"\n\n\t3.FILE MANAGER";
	cout<<"\n\n\n\n\n\n\n\n\n press ESC to exit";
	cout<<"\n\n\t\t\t\t\t\t\t\t\t\t\t\t                                          "<<date<<"."<<month(mon)<<"."<<year;
	cout<<" "<<daywk(day);
	_setcursortype(_NOCURSOR);
	while(1)
			{
			cho=getch();
			ch=cho-48;
			if(((ch<4)&&(ch>0))||(ch==-40)||(ch==-21))
			break;
			else
			sound(10000);
			delay(100);
			nosound();
			}
		switch(ch)
	{case 1:
		cleardevice();
			cout<<"\n\n\t\t      RECEPTIONIST"<<"\n\t\t      ------------ ";
		setbkcolor(LIGHTBLUE);
		file.open("patients.dat",ios::app|ios::binary|ios::out);
		kfile.open("patients.dat",ios::beg|ios::in|ios::binary|ios::out);
		kfile.seekg(0);
		cout<<"\n\n\n\n\t1.ADD A PATIENT";
		cout<<"\n\n\n\n\t2.ENTER APPOINTMENT\n\n\n\n\n\n\n\n\n\n\n\n\n\n";
			while(1)
			{
			cho=getch();
			ch=cho-48;
			if(((ch<3)&&(ch>0))||(ch==-40))
			break;
			else
			sound(10000);
			delay(100);
			nosound();
			}
			if(ch==-40)
			break;
		if(ch==-21)
		ext();
		fstream fyl("opnumbr.txt",ios::out|ios::in);
		int iopnum;
		switch(ch)
		{
		 case 1:
			cleardevice();
			setbkcolor(BLUE);
			fyl>>iopnum;
			++iopnum;
			fyl.close();
			dflag='y';
			patient pat(iopnum);
			fstream fyl("opnumbr.txt",ios::out|ios::in);
			fyl<<iopnum;
			fyl.close();
			cout<<"              ADD A PATIENT\n" <<"              ------------\n\n\n\n\n\n\n\n\n";
			pat.putdata(dflag,date,mon,year,day);
			file.write((char*)&pat,sizeof(pat));
			cout<<"  "<<pat.rname()<<"'S OP NUMBER IS :"<<iopnum<<"\n\n\n\n\n\n\n\n\n\n\n\n\n\n";
			file.close();
			kfile.close();
			getch();
			 sound(10000);
			delay(100);
			nosound();
			break;
		 case 2:
			cleardevice();
			setbkcolor(BLUE);
			_setcursortype(_SOLIDCURSOR);
			cout<<"\n\n\n\n\tENTER THE OP NO.";
			cin>>opnm;
			cout<<"\n\n\n\n\n\n\n\n\n\n\n\n\n\n" ;
			dflag='y';
			kfile.seekg(0);
			while((kfile)&&(kfile.read((char*)&pat,sizeof(pat))))
			{
			if(pat.opnumr()==opnm)
			 {

			  x=kfile.tellg();
			  pat.display(dflag,date,mon,year,day);
			  x=kfile.tellg();
			  kfile.seekp(x-sizeof(pat));
			  kfile.write((char*)&pat,sizeof(pat));
			  dflag='n';
			  break;
			 }
			}
			if(dflag=='y')
			cout<<"\n\n\n\n\tINVALID OP NO.!!!";
			file.close();
			kfile.close();
			getch();
			break;
			}
			break;




	 case 2: cleardevice();
		 setbkcolor(LIGHTBLUE);
		int cho,rmno;
		char ch,cch;
		cout<<"\n\n\n\n\n\n\n\n\n\n\n\t\t\tWARD MANAGER"<<"\n\t\t\t------------";
		cout<<"\n\n\t\t1.ADMIT PATIENT";
		cout<<"\n\n\t\t2.SEARCH PATIENT";
		cout<<"\n\n\t\t3.DISCHARGE PATIENT\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n";
		while(1)
			{
			cho=getch();
			ch=cho-48;
			if(((ch<4)&&(ch>0))||(ch==-40))
			break;
			else
			sound(10000);
			delay(100);
			nosound();
			}
			if(ch==-40)
			break;
		switch(ch)
		{

		case 1: cleardevice();
			setbkcolor(BLUE);
			_setcursortype(_SOLIDCURSOR);
			cout<<"\n\n\n\n\t\tENTER THE PATIENT'S OP NUMBER:";
			cin>>opnm;
			patient pat;
			dflag='y';
			kfile.open("patients.dat",ios::beg|ios::in|ios::binary|ios::out);
			kfile.seekg(0);
			while((kfile)&&(kfile.read((char*)&pat,sizeof(pat))))
			{if(pat.opnumr()==opnm)
			 {
			 x=kfile.tellg();
			 dflag='y';
			 break;
			 }
			}
			kfile.seekp(x-sizeof(pat));
			if(!(dflag=='y'))
			 {
			  cout<<"\n\n\tINVALID OP NUMBER!!!\n\n\n";
			 }
			if(dflag=='y')
			{
			char pr[15];
			cout<<"\n\n\n\n\t\tENTER THE REQUIRED WARD(A\B\C):";
			cin>>cch;
			cout<<"\n\n\n\n\t\tWHAT'S THE PROBLEM "<<pat.rname()<<" SUFFERING WITH ???";
			gets(pr);
			if(!((cch=='A')||(cch=='B')||(cch=='C')))
			 {
			  cout<<"\n\n\tINVALID WARD!!!\n\n\n";
			  break;
			 }
			rmno=ward(cch,opnm);
			opnm=pat.wrdadmtf(pr,date,mon,rmno,cch);
			kfile.write((char*)&pat,sizeof(pat));
			kfile.close();
			if(!opnm)
			{cout<<"\n\n\t"<<pat.rname()<<" IS ALREADY ADMITTED IN THIS HOSPITAL!!!\n\n\n";
			getch();
			break;
			}
			if(rmno)
			{
			cout<<"\n\t\t"<<pat.rname()<<"'S ROOM IS:"<<cch<<"-"<<rmno<<"\n\n\n\n\n\n\n\n\n";
			remove("ward.txt") ;
			rename("temp.txt","ward.txt");
			}
			else
			cout<<"\n\t\tNO ROOM!!!!\n\n\n\n\n\n\n\n\n";
			getch();
			}
			getch();
			break;


		 case 2:cleardevice();
			setbkcolor(BLUE);
			cout<<"\n\n\n\n\t\tSEARCH BY:";
			cout<<"\n\n\t\t\t1.NAME";
			cout<<"\n\n\t\t\t2.ADDRESS";
			cout<<"\n\n\t\t\t3.OP NUMBER";
			cout<<"\n\n\t\t\t4.PHONE NUMBER\n\n\n\n\n\n\n\n\n\n\n\n";
			while(1)
			{
			cho=getch();
			ch=cho-48;
			if(((ch<5)&&(ch>0))||(ch==-40))
			break;
			else
			sound(10000);
			delay(100);
			nosound();
			}
			_setcursortype(_SOLIDCURSOR);
			cleardevice();
			switch(ch)
			{ case 1:
				 cout<<"\n\n\n\n\t\tENTER THE PATIENT'S NAME:";
				 gets(name);

				 kfile.open("patients.dat",ios::beg|ios::in|ios::binary|ios::out);
				 kfile.seekg(0);
				 while((kfile)&&(kfile.read((char*)&pat,sizeof(pat))))
				 if(!strcmp(pat.rname(),name))
				 {
				  dflag='y';
				  opnm=pat.opnumr();
				 }
				if(!(dflag=='y'))
				{
				 cout<<"\n\n\tINVALID NAME!!!\n\n\n\n\n\n\n\n\n";
				 kfile.close();
				 break;
				}
				rmno=wsearch(opnm);
				if((rmno==0)&&(dflag=='y'))
				cout<<"\n\n\t"<<name<<" IS NOT ADMITTED IN THIS HOSPITAL!!!\n\n\n\n\n\n\n\n\n\n\n\n";
				admitfun(rmno);
				kfile.close();
				break;
			case 2: cout<<"\n\n\n\n\t\tENTER THE PATIENT'S ADDRESS:";
				 gets(name);
				 kfile.open("patients.dat",ios::beg|ios::in|ios::binary|ios::out);
				 kfile.seekg(0);
				 while((kfile)&&(kfile.read((char*)&pat,sizeof(pat))))
				 if(!strcmp(pat.raddrss(),name))
				 {
				  dflag='y';
				  opnm=pat.opnumr();
				  strcpy(name,pat.rname());
				 }
				if(!(dflag=='y'))
			       { cout<<"\n\n\tINVALID ADDRESS!!!";
				 kfile.close();
				 break;
				}
				rmno=wsearch(opnm);
				if((rmno==0)&&(dflag=='y'))
				cout<<"\n\n\t"<<name<<" IS NOT ADMITTED IN THIS HOSPITAL!!!";
				admitfun(rmno);
				kfile.close();
				break;

			case 3:	cout<<"\n\n\n\n\t\tENTER THE PATIENT'S OP NUMBER:";
				cin>>opnm;
				kfile.open("patients.dat",ios::beg|ios::in|ios::binary|ios::out);
				kfile.seekg(0);
				while((kfile)&&(kfile.read((char*)&pat,sizeof(pat))))
				if(pat.opnumr()==opnm)
				{
				dflag='y';
				strcpy(name,pat.rname());
				}
				if(!(dflag=='y'))
				{
				 cout<<"\n\n\tINVALID OP NUMBER!!!";
				 kfile.close();
				 break;
				}
				rmno=wsearch(opnm);
				if((rmno==0)&&(dflag=='y'))
				cout<<"\n\n\t"<<name<<" IS NOT ADMITTED IN THIS HOSPITAL!!!";
				admitfun(rmno);
				kfile.close();
				break;
			case 4: cout<<"\n\n\n\n\t\tENTER THE PATIENT'S PHONE NUMBER:";
				cin>>opnm;
				kfile.open("patients.dat",ios::beg|ios::in|ios::binary|ios::out);
				kfile.seekg(0);
				while((kfile)&&(kfile.read((char*)&pat,sizeof(pat))))
				if(pat.rphoneno()==opnm)
				{
				opnm=pat.opnumr();
				dflag='y';
				strcpy(name,pat.rname());
				}
				if(!(dflag=='y'))
				{
				 cout<<"\n\n\tINVALID PHONE NUMBER!!!";
				 kfile.close();
				 break;
				}
				rmno=wsearch(opnm);
				if((rmno==0)&&(dflag=='y'))
				cout<<"\n\n\t"<<name<<" IS NOT ADMITTED IN THIS HOSPITAL!!!";
				admitfun(rmno);
				kfile.close();
	 //	 case -40:      break;
				}
				break;

		 case 3:
			 _setcursortype(_SOLIDCURSOR);
			 cout<<"\n\n\n\n\t\tENTER THE PATIENT'S OP NUMBER:";
			 cin>>opnm;
			 dflag='n';
			 fstream kward,ktemp;
			 ktemp.open("temp.txt",ios::in|ios::out);
			 kward.open("ward.txt",ios::beg|ios::in|ios::out);
			 while(!(kward.eof()))
			 {
			  kward>>wp;
			  if(wp==opnm)
			   {dflag='y';
			    wp=0;
			    cout<<"\n\t\tDISCHARGED!!!";
			   }
			 ktemp<<wp<<" ";
			 }
			 if(!(dflag=='y'))
			{
			 cout<<"\n\n\tINVALID OP NUMBER!!!";
			 getch();
			 break;
			}
			else
			{kfile.open("patients.dat",ios::beg|ios::in|ios::binary|ios::out);
			 kfile.seekg(0);
			 while((kfile)&&(kfile.read((char*)&pat,sizeof(pat))))
			 if(pat.opnumr()==opnm)
			 {
			 opnm=pat.opnumr();
			 pat.dc(date,mon);
			 x=kfile.tellg();
			 kfile.seekp(x-sizeof(pat));
			 kfile.write((char*)&pat,sizeof(pat));
			 break;
			 }
			}
			kfile.close();
			 remove("ward.txt") ;
			 rename("temp.txt","ward.txt");
			 ktemp.close();
			 kward.close();
			 break;
			}
			getch();
			break;


  case 3:       cleardevice();
		setbkcolor(LIGHTBLUE);
		cout<<"\n\t\t\tFILE MANAGER"<<"\n\t\t\t-------------";
		cout<<"\n\n\t\t1.DELETE A PATIENT'S RECORD";
		cout<<"\n\n\t\t2.OBTAIN A PATIENT'S INFORMATION";
		cout<<"\n\n\t\t3.MODIFY PATIENT'S RECORD\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n";
	while(1)
			{
			cho=getch();
			ch=cho-48;
			if(((ch<4)&&(ch>0))||(ch==-40))
			break;
			else
			sound(10000);
			delay(100);
			nosound();
			}
			if(ch==-40)
			break;
		switch(ch)
		{
		 case 1:cleardevice();
			setbkcolor(BLUE);
			_setcursortype(_SOLIDCURSOR);
			cout<<"\n\n\n\n\t\tENTER THE PATIENT'S NAME:";
			gets(name);
			patient pat;
			kfile.open("patients.dat",ios::beg|ios::in|ios::binary|ios::out);
			kfile.seekg(0);
			char kflg='n';
			fstream temp1("temp.dat",ios::in|ios::out|ios::binary);
			while((kfile)&&(kfile.read((char*)&pat,sizeof(pat))))
			if(!strcmp(pat.rname(),name))
			 {  pat.display('p',date,mon,year,day);
			    cout<<"\n\t\tARE YOU SURE,YOU WANT TO DELETE THIS RECORD???(Y/N)";
			    dflag=getch();
			    sound(10000);
			    delay(100);
			    nosound();
			    kflg='y';
			    if((dflag=='N')||(dflag=='n'))
			    temp1.write((char*)&pat,sizeof(pat));
			 }
			else
			temp1.write((char*)&pat,sizeof(pat));

			if(kflg=='n')
			cout<<"\n\n\tRECORD NOT FOUND!!!\n\n\n\n\n\n\n\n\n\n\n\n";
			else
			{
			kfile.close();
			temp1.close();
			remove("patients.dat");
			rename("temp.dat","patients.dat");
			cout<<"\n\n\tDELETION SUCCESS!!!\n\n\n\n\n\n\n\n\n\n\n\n";
			}
			getch();
			break;
		case 2: cleardevice();
			setbkcolor(LIGHTBLUE);
			cout<<"\n\n\n\n\t\tSEARCH BY:";
			cout<<"\n\n\t\t\t1.NAME";
			cout<<"\n\n\t\t\t2.ADDRESS";
			cout<<"\n\n\t\t\t3.OP NUMBER";
			cout<<"\n\n\t\t\t4.PHONE NUMBER\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n";
		while(1)
			{
			cho=getch();
			ch=cho-48;
			if(((ch<5)&&(ch>0))||(ch==-40))
			break;
			else
			sound(10000);
			delay(100);
			nosound();
			}
			if(ch==-40)
			break;
			_setcursortype(_SOLIDCURSOR);
			cleardevice();
			switch(ch)
			{ case 1:
				 cout<<"\n\n\n\n\t\tENTER THE PATIENT'S NAME:";
				 gets(name);
				 dflag='n';
				 kfile.open("patients.dat",ios::beg|ios::in|ios::binary|ios::out);
				 kfile.seekg(0);
				 while((kfile)&&(kfile.read((char*)&pat,sizeof(pat))))
				 if(!strcmp(pat.rname(),name))
				 {
				 dflag='y';
				 pat.display('m',date,mon,year,day);
				 break;
				 }
				if(!(dflag=='y'))
				cout<<"\n\n\tINVALID NAME!!!\n\n\n\n\n\n\n\n\n\n\n\n";
				kfile.close();
				getch();
				break;
			case 2: cout<<"\n\n\n\n\t\tENTER THE PATIENT'S ADDRESS:";
				 gets(name);
				 kfile.open("patients.dat",ios::beg|ios::in|ios::binary|ios::out);
				 kfile.seekg(0);
				 while((kfile)&&(kfile.read((char*)&pat,sizeof(pat))))
				 if(!strcmp(pat.raddrss(),name))
				 {
				 dflag='y';
				 pat.display('m',date,mon,year,day);
				 break;
				 }
				if(!(dflag=='y'))
				cout<<"\n\n\tINVALID ADDRESS!!!\n\n\n\n\n\n\n\n\n\n\n\n";
				kfile.close();
				getch();
				break;

			case 3:	_setcursortype(_SOLIDCURSOR);
				cout<<"\n\n\n\n\t\tENTER THE PATIENT'S OP NUMBER:";
				cin>>opnm;
				dflag='n';
				kfile.open("patients.dat",ios::beg|ios::in|ios::binary|ios::out);
				kfile.seekg(0);
				while((kfile)&&(kfile.read((char*)&pat,sizeof(pat))))
				if(pat.opnumr()==opnm)
				{

				 dflag='y';
				 pat.display('m',date,mon,year,day);
				 break;
				}
				if(!(dflag=='y'))
				cout<<"\n\n\tINVALID OP NUMBER!!!\n\n\n\n\n\n\n\n\n\n\n\n";
				kfile.close();
				getch();
				break;
			case 4: cout<<"\n\n\n\n\t\tENTER THE PATIENT'S PHONE NUMBER:";
				cin>>opnm;
				kfile.open("patients.dat",ios::beg|ios::in|ios::binary|ios::out);
				kfile.seekg(0);
				dflag='n';
				while((kfile)&&(kfile.read((char*)&pat,sizeof(pat))))
				if(pat.rphoneno()==opnm)
				{

				 dflag='y';
				 pat.display('m',date,mon,year,day);
				 break;
				}
				if(!(dflag=='y'))
				cout<<"\n\n\tINVALID PHONE NUMBER!!!\n\n\n\n\n\n\n\n\n\n\n\n";
				kfile.close();
				}
				getch();
				break;
		case 3:cleardevice();
		       setbkcolor(LIGHTBLUE);
			_setcursortype(_SOLIDCURSOR);
		       cout<<"\n\n\tENTER THE PATIENT'S OP NUMBER  ";
		       cin>>opnm;
		       cleardevice();
		       int pos;
		       dflag='n';
		       kfile.open("patients.dat",ios::beg|ios::in|ios::binary|ios::out);
		       kfile.seekg(0);
		      while((kfile)&&(kfile.read((char*)&pat,sizeof(pat))))
		      if(pat.opnumr()==opnm)
		      {  pos=kfile.tellg();
			 dflag='y';
			 pat.display('l',date,mon,year,day);
			 break;
		      }
		       if(!(dflag=='y'))
		       {cout<<"\n\n\tINVALID OP NUMBER!!!";
			getch();
			break;
		       }
		       else
		       {
		       if(dflag=='y')
		       cout<<"\n\n\tDO YOU REALLY WANT TO MODIFY THIS RECORD???(Y/N)";
		       dflag=getch();
			sound(10000);
			delay(100);
			nosound();
		       if(!(dflag=='y'||dflag=='Y'))
		       break;
		       kfile.seekp(pos-sizeof(pat));
		       pat.putdata('c',date,mon,year,day);
		       cleardevice();
		       kfile.write((char*)&pat,sizeof(pat));
		       pat.display('c',date,mon,year,day);
		       cout<<"\n\n\tMODIFIED!!!\n\n";
		       getch();
		       kfile.close();
		       break;
		      }
		       }break;
      case -21:    cleardevice();
		    ext();
		    break;

	       } }
	       while(1);

	       }
void ext()
{
  cleardevice();
  setbkcolor(LIGHTBLUE);
  char ch;
  cout<<"\n\n\n\n\t\tDO YOU REALLY WANT TO QUIT(Y\\N)???\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n";
while(1)
{

ch=getch();
if((ch=='y')||(ch=='Y'))
exit(0);
if((ch=='N')||(ch=='n'))
break;
else
sound(10000);
delay(100);
nosound();
}
}
int ward(char wrd='p',long int wop=0)
{
  fstream tate,ward,temp;
  int flag=1;
  ward.open("ward.txt",ios::in|ios::out);
  temp.open("temp.txt",ios::in|ios::out);
  if(!ward)
  cout<<"cant open d fyl";
  int n=1;
  long int wp=10,r=1;
  if(wrd=='A')
 {
  while(!ward.eof())
  {
    ward>>wp;
    if((wp==0)&&(n<50)&&(flag))
    {temp<<wop<<' ';
    flag=0;
    }
    temp<<wp<<" ";
    ++r;
    if(r==149)
    return n;
    if(flag)
    ++n;
   }
  }      char s;
   if(wrd=='B')
   while(!ward.eof())
   {
    ward>>wp;
    if((wp==0)&&(n>=50)&&(n<100)&&(flag))
    {temp<<wop<<' ';
    flag=0;
    }
    temp<<wp<<" ";
    ++r;
    if(r==149)
    return (n-49);
    if(flag)
    ++n;
    }
   if(wrd=='C')
   while(!ward.eof())
   {ward>>wp;
    if((wp==0)&&(n<150)&&(n>=100)&&(flag))
    {temp<<wop<<' ';
    flag=0;
    }
    temp<<wp<<" ";
    ++r;
    if(r==149)
    return (n-99);
    if(flag)
    ++n;
   }
   return 0;
  }

long int wsearch(long int wop=0)
{fstream sward("ward.txt",ios::in|ios::out);
 long int wp=10;
 int n=1;
 while(!sward.eof())
  {
    sward>>wp;
    if(wp==wop)
    return n;
    ++n;
   }
   return 0;
}

void admitfun(int roomno)
{

 if(roomno)
 {
 if(roomno<50)
 cout<<"\t\tROOM IS: A-"<<roomno;
 if((roomno>=50)&&(roomno<100))
 cout<<"\t\tROOM IS: B-"<<roomno-49;
 if((roomno>=100)&&(roomno<150))
 cout<<"\t\tROOM IS: C-"<<roomno-99;
 }
}
char*month(int m)
{
  switch(m)
  {
    case 1:return "JAN";
    case 2:return "FEB";
    case 3:return "MAR";
    case 4:return "APR";
    case 5:return "MAY";
    case 6:return "JUN";
    case 7:return "JUL";
    case 8:return "AUG";
    case 9:return "SEP";
    case 10:return "OCT";
    case 11:return "NOV";
    case 12:return "DEC";
  }     }

char*daywk(int m)
{
  switch(m)
  {
    case 0:return "SUNDAY";
    case 1:return "MONDAY";
    case 2:return "TUESDAY";
    case 3:return "WEDNESDAY";
    case 4:return "THURSDAY";
    case 5:return "FRIDAY";
    case 6:return "SATURDAY";

  }     }
void pmd(int x,int y=0)
{
if(y==1)
{line(6*x, 7*x, 6*x,x* 5);
   line(6*x, x*5, 8*x,x* 5);
   line(7*x, x*5, 7*x, x*7);
   line(x*8, 5*x, 8*x, 7*x);
   if(x>10)
   {
   line(x*7, 4*x, 7*x, 3*x);
   line(x*6.65, 1.75*x, 5*x, 0.78*x);
   line(x*7.35, 1.75*x, 9*x, 0.78*x);
   }}
   line(x*4, 7*x, 4*x, 9*x);
   line(x*4, 5*x, 5.5*x, 5*x);
   line(x*5.5, 7*x, 5.5*x, 5*x);
   line(x*4, 7*x, 5.5*x, 7*x);
   line(x*8.5, 5*x, 10*x, 5*x);
   line(x*8.5, 7*x, 10*x, 7*x);
   line(x*8.5, 7*x, 8.5*x, 5*x);
   line(x*10, 2*x, 10*x, 5*x);
 }


PRO_HDM(GRPH).CPP
