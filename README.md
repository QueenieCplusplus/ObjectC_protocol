# ObjectC_protocol
Object C 添增協定，以實現類別的多重繼承功能

協定事實上是一組方法列表，不依賴於特定類別，使用協定可以使不同類別共用相同訊息。
很類似後來 swift 的 delegate 委派功能。

宣告協定
 
                   @protocol 協定名稱
                   
                   @end
                   
聲明方法

                   @protocol 協定名稱
                   
                   @required 
                   實現協定的必須方法
                   如無指定關鍵字，則協定中宣告的方法預設為必須實現。
                   
                   @end
                   
KKK.h
協定

                  #import <Foundation/Foundation.h>
                  @protocol 協定名稱叫KKK
                  
                  -(void)go;   ------------------------------------
                  @end                                            |
                                                                  |
                                                                  |
                                                                被QQQ.h繼承
XXX.h                                                             
介面                                                               
實行協定                                                            
                                                                 
                   #import <Foudation/Foundation.h>               
                   #import "KKK"      ----------------------
                                                            實施協定
                   @interface QQQ: NSObject<KKK> --------
                   {
                   
                      int p;
                   
                   }
                   
                   -(void)setP;
                   -(void)printP;
                   
                   @end


QQQ.h
建置類別
實作方法
一但介面實施協定
則協定中的必須方法必定需要實作

                 #import"QQQ.h"
                 
                 @implementation QQQ
                 
                 -(void) setP
                 {
                 
                    p=99;
                 
                 }
                 
                 -(void) printP
                 {
                 
                    NSlog(@"%i", p);
                 
                 }
                 
                 -(void)go               -------
                 {                              |
                    NSLog(@"go");          繼承協定的方法
                                                |  
                 }                       -------
                  
                 @end

main.m

                #import<Foundation.Foundation.h>
                #import"QQQ.h"
                
                int main(int argc, const char * argv[])
                {
                
                   QQQ *q=[[QQQ alloc]init];
                   
                   //call functions
                   [q setP];
                   [q printP];
                   [q go]; -------------------> 協定方法被輾轉繼承
                                                倘若 go() 方法沒有被實施
                                                則會出現警告訊息
                
                   return 0;
                }


同時實施多個協定時
實施方式

                  #import"協定1.h"
                  #import"協定2.h"
                  #import"協定3.h"
                  
                  @interface QQQ: NSObject<協定1, 協定2, 協定3>
                  
                    //...
                    
                  @end

               
