# fusion_detail_2D

fusion_detail_2D

%%function section: 2D fusion rule based on Guo and Yan (2017) algorithm for fused gravity & magnetic data

%%Code Rewritten by: Sara Nasri and Amin Roshandel kahoo

%%Tel:+98 23 3239 5509; Email address:roshandel@shahroodut.ac.ir

function Dm = fusion_detail_2D(a,b,r)

Dm=zeros(size(a));

[row1,col1]=size(a);

Dm11=zeros(row1+(2*r),col1+(2*r));

[row11,col11]=size(Dm11);

Dm11(r+1:row11-r,r+1:col11-r)=a;

Dm22=zeros(row1+(2*r),col1+(2*r));

Dm22(r+1:row11-r,r+1:col11-r)=b;

for i=1+r:row1+r

    for j=1+r:col1+r
    
        w1=Dm11(i-r:i+r,j-r:j+r);
        
        w2=Dm22(i-r:i+r,j-r:j+r);
        
        aa=zeros(size(w1));
        
        bb=aa;
        
        aa(abs(w1)>abs(w2))=2;
        
        bb(abs(w2)>abs(w1))=2;
        
        aa(abs(w1)==abs(w2))=1;
        
        bb(abs(w1)==abs(w2))=1;
        
        Nm1=sum(aa(:));
        
        Nm2=sum(bb(:));
        
        if Nm1>Nm2
        
            Dm(i-r,j-r)=w1(r+1,r+1);
            
        elseif Nm2>Nm1
        
            Dm(i-r,j-r)=w2(r+1,r+1);
            
        elseif Nm2==Nm1
        
            if abs(w1(r+1,r+1))>=abs(w2(r+1,r+1))
            
                Dm(i-r,j-r)=w1(r+1,r+1);
                
            else
            
                Dm(i-r,j-r)=w2(r+1,r+1);
                
            end
            
        end
        
    end
    
end

end
