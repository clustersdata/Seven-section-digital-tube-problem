# Seven-section-digital-tube-problem

Seven section digital tube problem

	从一个数字变化到其相邻的数字只需要通过某些段(数目不限)
  
    1	     或拿走某些段(数目不限)来实现.但不允许既增加段又拿起段.
    
  ┏━┓     例如:3可以变到9,也可以变到1
  
 6┃ 7┃2	 ━┓	 ┏━┓ 	     ━┓      ┃
 
  ┣━┫	   ┃	 ┃  ┃ 	       ┃      ┃
  
 5┃  ┃3	 ━┫ → ┗━┫ 	     ━┫  →  ┃
 
  ┗━┛	   ┃	     ┃ 	       ┃      ┃
  
    4		 ━┛	   ━┛ 	     ━┛      ┃
    

要求:(1)判断从某一数字可以变到其它九个数字中的哪几个.

     (2)找出一种排列这十个数字的方案,便这样组成的十位数数值最小.
     
type kkk=set of 0..9;

const a:array[-1..9] of set of 1..7

	=([5,6],[1,2,3,4,5,6],[2,3],[1,2,4,5,7],[1,2,3,4,7],[2,3,6,7],
  
	  [1,3,4,6,7],[1,3,4,5,6,7],[1,2,3],[1,2,3,4,5,6,7],[1,2,3,4,6,7]);
    
var

   i,j:integer;
   
   b:array[-2..9] of set of 0..9;
   
procedure number(p:string;s,l:integer;k:kkk);

  {P:生成的数;s:用了几个数字;i:前一个是哪个数字;k:可用的数字}
  
var i:integer;

begin

     for i:=0 to 9 do
     
	 if (i in k) and ( i in b[l]) then begin
   
	 {数字i未用过,且i可由前一个采用的数字变化而来}
   
	    if s=10 then begin writeln('Min:',p,i);readln;halt;end
      
	       else number(p+chr(48+i),s+1,i,k-[i]);
         
	 end;
   
end;


begin

     for i:=1 to 9 do b[i]:=[];
     
     b[-2]:=[0..9];
     
     for i:=-1 to 8 do
     
	 for j:=i+1 to 9 do
   
	     if (a[i]<=a[j]) or (a[j]<=a[i]) then begin
       
		b[i]:=b[i]+[j];
    
		b[j]:=b[j]+[abs(i)];
    
	     end;
       
	 b[1]:=b[1]+b[-1];
   
     for i:=0 to 9 do begin
     
	 write(i,' may turn to :');
   
	 for j:=0 to 9 do if  j in b[i] then write(j,' ');
   
	 writeln;
   
     end;
     
     number('',1,-2,[0..9]);
     
End.

