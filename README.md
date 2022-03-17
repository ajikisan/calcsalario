<h1> Programação Natural </h1>

No período de 17/01/2022 a 16/03/2022

Houve curso de Programação Natural I e II com o instrutor William Moura Machado.

Realizei mais de 85 programas.

CS CalcSalário é um dos projetos que fiz no qual foi abordado vários assuntos
Program, Subroutine, Function, Data Areas, Map e Helproutine utilizados no curso.

>                                       > +  Program     NT2MAM03 Lib NAT2CUR  
 Top    ....+....1....+....2....+....3....+....4....+....5....+....6....+....7..
   0010 ** FUNCAO DO PROGRAMA..: CALCULAR REMUNERAÇÃO SALARIAL     
   0020 ** NOME DO PROGRAMA....: NT2MAM03 - MAPA CHAVEUSU - NT2MAMH3 - NT2MAMCS 
   0030 ** AGORA SIM! O APLICATIVO CS CALCSALáRIO FOI DESENVOLVIDO PARA         
   0040 ** AJUDAR VOCê A SIMULAR O CáLCULO DA REMUNERAçãO SALARIAL.             
   0050 ** ALTERE OS DADOS E SAIBA OS VALORES AUTOMATICAMENTE.                  
   0060 ** ANALISTA............: MIRIAN AJIKI MOLICAWA                          
   0070 ** DATA CRIACAO........: 14/02/2022                                     
   0080 ** INSTRUTOR...........: WILLIAM MOURA MACHADO                          
   0090 ** OBJETIVO: PROGRAMAÇÃO NATURAL PARA MAINFRAME                         
   0100 ** NT2MAMH3 - EXEMPLO DE CRIACAO DE SUBROTINA                           
   0110 ** NT2MAMCS - MAPA NO QUAL SÓ EXIBE A MENSAGEM DO CS-CALCSALÁRIO        
   0120 ** --------------------------------------------------------------------*
   0130 DEFINE DATA                                                             
   0140 LOCAL                                                                   
   0150 01 #DATA(A10)                                                           
   0160 01 #HORA(A8)                                                            
   0170 01 #PROGRAMA(A8)                                                        
   0180 01 #USUARIO(A8)                                                         
   0190 01 #NOME-FUNC(A40)                                                      
   0200 01 #VLR-SALARIO(N9,2)                                                   
   0210 01 #QTD-DIA-NORMAL(N2)                                                  
   0220 01 #QTD-HR-EXTRA-NORMAL(N2)                                             
   0230 01 #QTD-HR-EXTRA-FERDOM(N2)                                             
   0240 01 #QTD-TOT-HR-TRAB(N4)                                                 
   0250 01 #VLR-HR-NORMAL(N5,2)                                                 
   0260 01 #VLR-HR-EXTRA(N5,2)                                                  
   0270 01 #VLR-HR-FERDOM(N5,2)                                                 
   0280 01 #VLR-REMUNERADO(N8,2)                                                
   0290 END-DEFINE                                                              
   0300 * SET CONTROL 'YS'                                                      
   0310 SET KEY PF1=HELP NAMED 'AJUDA' PF3='FIN' NAMED 'SAI'                    
   0320 PF5='%.' NAMED 'ENCERRA'                                                
   0330 MOVE *DAT4E TO #DATA                                                    
   0340 MOVE *TIME TO #HORA                                                     
   0350 MOVE *PROGRAM TO #PROGRAMA                                              
   0360 MOVE *INIT-USER TO #USUARIO                                             
   0370 REPEAT                                                                  
   0380   INPUT WITH TEXT 'Olá, complete as linhas e pressione '-               
   0390     'a tecla "ENTER", por gentileza.' USING MAP 'CHAVEUSU'              
   0400   IF #NOME-FUNC EQ ' '                                                  
   0410     REINPUT 'Digite o nome do funcionário' MARK *#NOME-FUNC ALARM       
   0420   END-IF                                                                
   0430   IF #VLR-SALARIO LT 0                                                  
   0440     REINPUT 'Digite o valor do salário' MARK *#VLR-SALARIO ALARM        
   0450   END-IF                                                                
   0460   IF #QTD-HR-EXTRA-NORMAL LT 0                                          
   0470   REINPUT 'Digite a quantidade de horas extras realizadas em dia normal'
   0480       MARK *#QTD-HR-EXTRA-NORMAL ALARM                                  
   0490   END-IF                                                                
   0500   IF #QTD-DIA-NORMAL LT 0                                               
   0510     REINPUT 'Digite a quantidade de dias normais trabalhados'           
   0520       MARK  *#QTD-DIA-NORMAL ALARM                                      
   0530   END-IF                                                                
   0540   IF #QTD-HR-EXTRA-FERDOM LT 0                                          
   0550     REINPUT 'Digite a quantidade de horas trabalhadas em sábados, '-    
   0560       'domingos e/ou feriados'                                          
   0570       MARK *#QTD-HR-EXTRA-FERDOM ALARM                                  
   0580   END-IF                                                                
   0590   PERFORM FOLHA-PAGAMENTO                                               
   0600 END-REPEAT                                                              
   0610 ** SUBROTINA INTERNA                                                    
   0620 DEFINE SUBROUTINE FOLHA-PAGAMENTO                                       
   0630 ** TOTAL DE HORAS TRABALHADAS                                           
   0640 *                                                                       
   0650 #QTD-TOT-HR-TRAB := (#QTD-DIA-NORMAL * 8) + #QTD-HR-EXTRA-NORMAL +      
   0660   #QTD-HR-EXTRA-FERDOM                                                  
   0670 *                                                                       
   0680 *                                                                       
   0690 ** VALOR HORA NORMAL                                                    
   0700 *                                                                       
   0710 #VLR-HR-NORMAL := #VLR-SALARIO / 220                                    
   0720 *                                                                       
   0730 **VALOR HORA-EXTRA                                                      
   0740 #VLR-HR-EXTRA := #VLR-HR-NORMAL + ((#VLR-HR-NORMAL*50)/100)             
   0750 *                                                                       
   0760 **VALOR HORA-EXTRA FERIADO/DOMINGO                                      
   0770 #VLR-HR-FERDOM := #VLR-HR-NORMAL + ((#VLR-HR-NORMAL* 100)/100)          
   0780 *                                                                       
   0790 **VALOR REMUNERADO                                                      
   0800 *                                                                       
   0810 #VLR-REMUNERADO := (#VLR-HR-NORMAL * (#QTD-DIA-NORMAL * 8)) +           
   0820   (#VLR-HR-EXTRA * #QTD-HR-EXTRA-NORMAL) +                              
   0830   (#VLR-HR-FERDOM * #QTD-HR-EXTRA-FERDOM)                               
   0840 END-SUBROUTINE                                                          
   0850 END                                                                     
        ....+....1....+....2....+....3....+....4....+....5....+... S 85   L 66  





>                                       > +  Helproutine NT2MAMH3 Lib NAT2CUR  
Top    ....+....1....+....2....+....3....+....4....+....5....+....6....+....7..
  0010 ** FUNCAO DO PROGRAMA...: HELPROUTINE - NT2MAM03 
  0020 ** NOME DO PROGRAMA.....: NT2MAMH3                                      
  0030 ** ANALISTA.............: MIRIAN AJIKI MOLICAWA                         
  0040 ** DATA CRIACAO.........: 16/02/2022                                    
  0050 ** INSTRUTOR............: WILLIAM MOURA MACHADO                         
  0060 ** SE UTILIZADO ESTE EXEMPLO AO CLICAR A TECLA F1 PARA AJUDA.              
  0070 ** SERÁ EXIBIDA UMA MENSAGEM NA JANELA COM O TEXTO SOBRE O QUE É O SISTEMA 
  0080 ** E PARA OS DEMAIS CAMPO QUE NãO HAVERá AJUDA DISPONíVEL.                  
  0090 ** -------------------------------------------------------------------  
  0100 DEFINE DATA                                                             
  0110 PARAMETER                                                               
  0120 01 #CAMPO(A65)                                                          
  0130 LOCAL                                                                   
  0140 01 #MENSAGEM(A65)                                                       
  0150 END-DEFINE                                                              
  0160 * COMPRESS 'AJUDA INDISPONíVEL PARA O CAMPO' #CAMPO TO #MENSAGEM        
  0170 DEFINE WINDOW HELP1                                                     
  0180 SIZE 14*65                                                              
  0190 BASE 10/8                                                               
  0200 SET WINDOW 'HELP1'                                                      
  0210 WRITE NOTITLE                                                           
  0220 '                       Agora Sim!'                                     
  0230 '                       ----------'                                     
  0240 '    O aplicativo CS CalcSalário foi desenvolvido para '                
  0250 ' ajudar você a simular o cálculo da remuneração salarial.'             
  0260 '   Altere os dados e saiba os valores automaticamente.    '            
  0270 '----------------------------------------------------------'            
  0280 '----------------------------------------------------------'            
  0290 ' CS CalcSalário'                                                       
  0300 ' Build Feb 14 2022 Version 1.0'                                        
  0310 ' Natural For Mainframes       '                                        
  0320 ' https://github.com/ajikisan  '                                        
  0330 * #MENSAGEM                                                             
  0340 END                                                                     
       ....+....1....+....2....+....3....+....4....+....5....+... S 34   L 15  
                                                                             
                                                      
 
 
Fonte:

Material: Curso Básico de Programação Natural - Autor - Luciano Perdigão 

O Natural é uma ferramenta de desenvolvimento de 4ª geração desenvolvida pela
Software AG (Alemanha) e distribuída no Brasil pela Consist. 
Além de possuir a versão para MVS, objeto deste curso, possui versões para UNIX, OS/2 e Windows.
Algumas características do Natural são:
• Linguagem de programação com acesso a diversos bancos de dados: ADABAS (Hierárquico e relacional), Oracle, Db2, etc.;
• Utiliza diversos editores para criar programas, funções, telas pré-formatadas e áreas de dados;
• Permite uma programação modularizada;
• Utiliza funções e variáveis do sistema;
• Permite execução on-line e batch;
• Possui utilitário de testes de programação;
• Possui utilitário de criação/manutenção de mensagens de erros de aplicação;
• Qualquer aplicação pode ser facilmente portada para várias outras plataformas.
Os objetos Natural (programas, mapas, áreas de dados, etc.) são armazenados em
bibliotecas (“Libraries”), com estrutura parecida com o diretório DOS e podem ter 8 caracteres
como nome máximo. Mesmo sendo objetos de diferentes tipos, não podem possuir o mesmo
nome.
As principais vantagens do NATURAL em relação às linguagens tradicionais são:
• Maior facilidade de acesso a Banco de Dados (ADABAS, DB2, ORACLE, etc...);
• Maior velocidade de programação;
• Maior dinamismo em testes e manutenção de programas; e
• Menor preocupação com os demais recursos da instalação.
