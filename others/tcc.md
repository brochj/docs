# _BIBLIOGRAFIA -  TCC_

## Conteúdo
[I   - Dissertações](#i---dissertações)  
[II  - Teses](#ii---teses)  
[III - Artigos](#iii---artigos)  
[IV  - TCCs](#iv---tccs)  
[V   - Tutoriais e Projetos](#v---tutoriais-e-projetos)  
[VI  - Tutoriais e Projetos que não são específicos para detecção de velocidade, porém podem ajudar](#vi---tutoriais-e-projetos-que-não-são-específicos-para-detecção-de-velocidade)  
[VII - Livros](#vii---livros)  
[Ver Depois](#ver-depois)


# [I - Dissertações](#conteúdo)

1. [**Dissertação**, 1997] - [Deteccção de movimento e sua aplicacação á monitorização de tráfego][Dissertacao_1]  
**[06/07/18 - Broch] _- É interresante pra poder começar a escrever a introdução do TCC._**

[Dissertacao_1]:https://repositorio-aberto.up.pt/bitstream/10216/11449/2/Texto%20integral.pdf

---
2. [**Dissertação**, 2003] - [Um Equipamento Eletrônico de Monitoramento de Velocidade](https://www.lume.ufrgs.br/bitstream/handle/10183/6139/000437283.pdf?seq)  
**[06/07/18 - Broch] _- Apresenta os meios de medição de velocidade e propõe um radar utilizando processamento de imagem._**

	>"Uma câmera fica permanentemente filmando a via pública. Esta câmera deve ser capaz de gerar imagens entrelaçadas, pois o princípio para o cálculo é justamente a difereça de varredura entre as linhas ímpares e pares."

---
3. [**Dissertação**, 2015] - [Medição de posição, velocidade e aceleração utilizando
visão computacional em robôs móveis.](http://repositorio.uema.br/bitstream/123456789/160/1/EDUARDO%20HENRIQUE%20CASTRO%20MENDES.pdf)

	>"Este trabalho objetiva o desenvolvimento de um sistema para localização e medições de um robô móvel baseada em técnicas de visão computacional utilizando a **biblioteca OpenCV**. O sistema captura imagens de um robô móvel em um plano a partir de uma câmera montada no teto do ambiente."

4. [**Dissertação**, 72 págs, 2012 ] - [Identificação de tipos de veículos em videos de trânsito](http://www.decom.ufop.br/pos/site_media/uploads_ppgcc/publicacao/rensso2012.pdf)  
**[20/07/18 - Broch] _- Na pág(3) tem uma parte  de como pode ser classificado o SMBV (em 3 tipos). Pode ser interessante para colocar na introdução_**  
**[20/07/18 - Broch] _- Exemplo de Objetivos, e objetivos específicos_**    
**[20/07/18 - Broch - OK] _- O SIT pode ser classificado de acordo com a instalação das câmeras, em movimento ou estáticas_**  
**[20/07/18 - Broch] _- Problemas de Captura, Vibrações da câmera, Qualidade da imagem, Compressão do vídeo, Limpeza das lentes, posição das câmeras, Rede de envio de dados_**  
**[20/07/18 - Broch] _- Subtração de fundo: Background pode ser divido em Métodos não recursivo e Recursivos._**   
**[23/07/18 - Broch] _- Nesse trabalho é apresentado um método de geração progressiva da imagem de fundo._**  
**[23/07/18 - Broch] _- No Cap.(5) descreve as etapas para utilizar o_ Scale-invariant feature transform (SIFT).**  
**[24/07/18 - Broch -  OK] _- Máquina de Vetores de Suporte (SVM - Support Vector Machine) é um classificador que separa conjuntos de objetos em grupos, separando-os por uma linha, que pode ser linear ou não linear._**  
**[24/07/18 - Broch] _- Na pág 44 apresenta todo o fluxograma do modelo proposto._**   
**[24/07/18 - Broch] _- Na pág 58 cita as principais_** DESVANTAGENS **_encontradas utilizando o modelo proposto._**  

	>Os Sistemas Inteligentes de Transporte (**SIT**) são os encarregados de fazer o controle e monitoramento do tráfego. ....Realizam tarefas como: determinação do fluxo veicular, detecção de acidentes, monitoramento do tráfego, controle de velocidade, reconhecimento, contagem e/ou identificação de veículos.

	> Uma solução inovadora dentro dos **SITs** são os Sistemas de Monitoramento Baseados em Vídeo (**SMBV**).

	>Devido à grande quantidade de variações do ambiente o método para extrair as características foi o SIFT, dado que ele se adequa melhor a nosso problema. O SIFT descreve a imagem de forma local, para poder utilizar a informação do descritor a informação é organizada em um vocabulário visual. Finalmente o classificador utilizado é o SVM.

	> **Modelo proposto**: Geração da imagem de fundo >> Subtração da imagem de fundo >> Pré-processamento das imagens >> Extração das características >> Geração dos _clusters_ >> histograma dos _clusters_ >> Classificador SVM. 

---
# [II - Teses](#conteúdo)

1. [**Tese**, 2003] - [Metodologia para detecção rápida de movimento em sequência de imagens](http://www.teses.usp.br/teses/disponiveis/76/76132/tde-05052008-173600/publico/IsauraOliveira_D.pdf)  
**[09/07/18 - Broch] _- Ver sobre o Diagrama de Agulhas_**

---
# [III - Artigos](#conteúdo)

1. [**Artigo**, 2014] - [Proposal a Vehicle Speed Measuring System Using Image Processing](https://ieeexplore.ieee.org/document/6845938/?reload=true)  
**[11/07/18 - Broch] _- Preciso baixar da base de dados do IEEE_**

	>This approach is aimed **to improve the vehicle speed measuring accuracy at night**. ... the image based vehicle speed measuring system for dark environment was not developed by now. .... **Experiment result shows a reasonable measuring value.**

---
2. [**Artigo**, 2011] - [Speed Detection Camera System using Image Processing Techniques on Video Streams](http://www.ijcee.org/papers/418-E1077.pdf)

---
3. [**Artigo**, 2015] - [Vehicle Speed Measurement and Number Plate Detection using
Real Time Embedded System](https://1drv.ms/b/s!AhcmkAvgs28vgZsVXPsmwasrx4werQ)  
**[09/07/18 - Broch] _- Tem uma parte interessante onde diz para dividir a faixa de rodagem em regiões, afim de conseguir minimizar processamento computacional._**  

---
4. [**Artigo**] - [Processamento de Imagens: Métodos e Análises](http://www.cbpf.br/cat/pdsi/pdf/ProcessamentoImagens.PDF)
	
	>"Neste artigo procuramos dar uma visão da área de processamento digital de imagens e suas aplicações. Abordamos conceitos importantes sobre a representação espacial de um pixel, a **medida de distâncias**, a segmentação de uma imagem e o reconhecimento de formas. Utilizamos situações reais para exemplificarmos as técnicas apresentadas. É nosso objetivo **abordar de forma introdutória e simplificada o tema**.¨

---
5. [**Artigo**, 2014] - [Mensuração da velocidade de deslocamento de corpos rígidos em tempo real por análise de sequência de imagens e pela transformação empírica baseada nas funções polinomiais](http://seer.upf.br/index.php/rbca/article/download/2857/2556)  
**[13/07/18 - Broch] _- Tem um capítulo referente à "Segmentação de corpos em movimento pela média de Bradski"._**  
**[13/07/18 - Broch] _- Tem um capítulo bem curto referente à "Modelo polinomial 3D"._**

	>"Resumo: Este trabalho apresenta uma metodologia para mensurar a velocidade de um corpo rígido em movimento por meio da análise de sequências de imagens adquiridas por uma filmadora digital comercial. ... Esse resultado é obtido pela aplicação da técnica de segmentação **baseada na média temporal dos valores de brilho de cada pixel registrado em N quadros de imagens consecutivos**. Após a detecção e a segmentação dos corpos em movimento, alguns pontos dispostos sobre as suas imagens (pontos do espaço-imagem) são transformados em coordenadas métricas do espaço-objeto. ... Transformando os pontos desejados do plano-imagem (2D) para seus respectivos correspondentes no espaço-objeto (3D), a distância percorrida pelo corpo em um determinado intervalo de tempo pode ser calculada e, dessa forma, a velocidade de deslocamento do corpo é mensurada."

---
6. [**Artigo**, UTFPR, 2016] - [A Video-Based System for Vehicle Speed Measurment in Urban Roadways	](http://www.dainf.ct.utfpr.edu.br/~rminetto/projects/vehicle-speed/Paper_ITS_final.pdf)  
**[10/07/18 - Broch] _- Bem interessante, apresenta toda a metodologia de como funciona o radar e depois compara os resultados com um radar de Loop já instalado. Foi feito por professores da UTFPR de Curitiba. Nesse [SITE](http://www.dainf.ct.utfpr.edu.br/~rminetto/projects/vehicle-speed/) está disponível o DATASET e Códigos utilizados._**

	>"In this paper, we propose a non-intrusive, **videobased system for vehicle speed measurement** in urban roadways. Our system uses an optimized motion detector and a novel text detector to efficiently locate vehicle license plates in image regions containing motion. Distinctive features are then selected on the license plate regions, tracked across multiple frames, and rectified for perspective distortion. Vehicle speed is measured by comparing the trajectories of the tracked features to known real world measures. The proposed system was tested on a data set containing approximately five hours of videos recorded in different weather conditions by a single low-cost camera, ... . **The measured speeds have an average error of -0.5 km/h, staying inside the [-3,+2] km/h limit determined by regulatory authorities**..."

---
7. [**Artigo**, 2016] - [Vehicle classification and speed estimation using computer vision techniques](http://sedici.unlp.edu.ar/bitstream/handle/10915/56425/Documento_completo__.pdf-PDFA.pdf?sequence=3)  
**[11/07/18 - Broch] _- Foi utilizado OpenCV 3 e Python 2_**

	>**Abstract**: In this work, we implement a real-time vehicle classification and speed estimation system and apply it to videos acquired from traffic cameras installed in highways. In this approach we: a) **Detect moving vehicles through backgroundforeground segmentation techniques.** b) Compare different supervised classifiers (e.g. artificial neural networks) for vehicle classification into categories: (car, motorcycle, van, and bus/truck). c) Apply a calibration method to georeference vehicles using satellite images. d) **Estimate vehicles speed per class using feature tracking and nearest neighbors algorithms**

---
8. [**Artigo**, 2017] - [Development of prototype for vehicle speed measurement](https://ieeexplore.ieee.org/document/8256737/)  
**[11/07/18 - Broch] _- Preciso baixar da base de dados do IEEE_**  
	
	>**Abstract**: ...The vehicle speed is estimated using algorithm based on **background modeling and blob detection**. Absolute differencing method isolates foreground and background efficiently. The blob detection technique provides coordinates in the form of centroid resulting in the display of the vehicle movement.  

	>**The error in the speed estimation is observed to be 9 %.**

---
9. [**Artigo**, 2016] - [Speed detection using image processing](https://ieeexplore.ieee.org/document/7863015/)  
**[13/07/18 - Broch] _- Preciso baixar da base de dados do IEEE_**  
**[13/07/18 - Broch] _- Parece ser bem preciso, e é objetivo do TCC, utilizar uma camera em tempo real para medir a velocidade. Nesse conseguiram um erro bem baixo de 3%._** 

	>**Abstract**: In this paper we have come up with an alternative method of using image and video processing which can overcome the drawbacks of radar guns. The speed of vehicle is updated every half a second, hence keeping a track on acceleration and deceleration of vehicle in the field of view of the camera.  

	>**The speed calculated shows an error of only 3% in real time.** 

---
10. [**Artigo**, 2016] - [Vehicle detection and tracking techniques: a concise review](https://arxiv.org/ftp/arxiv/papers/1410/1410.5894.pdf)  
**[13/07/18 - Broch] _- É interessante pois apresenta os métodos mais utilizados._**  
**[13/07/18 - Broch] _- Por ser uma review, tem mais de 60 referências, então dá pra ter uma noção geral do já foi feito sem perder muito tempo._**

---
11. [**Artigo**, 5 pags, 2017] - [A review on vehicle speed detection using image processing](http://troindia.in/journal/ijcesr/vol4iss11part4/23-28.pdf)  
**[13/07/18 - Broch] _- É interessante pois é bem curto (5 páginas) e é baseado em 11 referências._** 

---
# [IV - TCCs](#conteúdo)

1. [**TCC**, 53 pág., 2016] - [Robô móvel com visão computacional usando a **biblioteca OpenCV** para seguimento de linha](http://www.cear.ufpb.br/arquivos/cgee/TCC/TCC_-_PEDRO_HENRIQUE_MEIRA_DE_ANDRADE.pdf)

	>" A plataforma utilizada é um pequeno robô móvel e dotado de uma câmera, capaz de seguir uma linha no chão. O controle cinemático é implementado em uma Raspberry Pi que também é responsável pelo processamento da imagem. A grande vantagem dessa metodologia é que com a câmera o robô pode adiantar prováveis curvas e alterar a velocidade e posição conforme a trajetória, tornando o movimento mais eficaz. Foi utilizada a **biblioteca OpenCV** que é a base para todo o tratamento da imagem e por consequência, do controle de velocidade e direção. O **acionamento dos motores** e a leitura dos sensores foram feitos usando a plataforma Arduino interligado a Raspberry Pi.

---
# [V - Tutoriais e Projetos](#conteúdo)

1. [**Tutorial**, 2017] - [Object Tracking using OpenCV (C++/Python)](https://www.learnopencv.com/object-tracking-using-opencv-cpp-python/)

	>In this tutorial, we will learn about **OpenCV tracking API** that was introduced in OpenCV 3.0. We will learn **how and when to use the 6 different trackers available in OpenCV 3.2** — BOOSTING, MIL, KCF, TLD, MEDIANFLOW, and GOTURN. We will also learn the general theory behind modern tracking algorithms.

---
2. [**Tutorial**, 2016] - [Real-time speed estimation of cars with OpenCV](https://www.amphioxus.org/content/real-time-speed-estimation-cars)  
**[10/07/18 - Broch] _- Apresenta a um forma de medir velocidade utilizando a biblioteca OpenCV C++. Não é tão passo a passo, mas apresenta alguns fluxogramas de como é o funcionamento. Tem os códigos no [BitBucket](https://bitbucket.org/amphioxus/vehicletracker3)._**
 
---
3. [**Tutorial**, 2015] - [Basic motion detection and tracking with Python and OpenCV Python](https://www.pyimagesearch.com/2015/05/25/basic-motion-detection-and-tracking-with-python-and-opencv/)  
**[11/07/18 - Broch] _- Pode ser bem útil para entender melhor e já começar testando. Apresenta a um  passo a passo de como utilizar o motion detection e tracking. Tem os códigos no explicados_**

	
	**[11/07/18 - Broch] _- Esse site [www.pyimagesearch.com](https://www.pyimagesearch.com/) é bom, tem vários tutoriais, a maioria tudo relacionado a processamento de imagem utilizando a bib OpenCV em Python._**

	**[14/07/18 - Broch - OK] _- Motion detection utiliza-se da técnica de background subtraction. Essa técnica de background subtraction é bastante utilizada em diversos tipos de aplicações de visão computacional. Exemplo como a contagem de carros que passam em uma rodovia, ou até mesmo a para saber o número de pessoas que entram e saem de uma loja._**

	**[14/07/18 - Broch - OK] _- Em motion detection é feita a seguinte suposição:._**  

	**[14/07/18 - Broch - OK] _- O segundo plano (background) do video é considerado como uma grande área estática e imutável durante uma sequência de frames do video analisado/monitorado. Sendo assim, tem-se o modelo do background como uma espécie de referência._**  

	**_Através da comparação dessa referência com os frames subsequentes, nomeados como primeiro plano (foreground), consegue-se idetificar mudanças substanciais, o que na caracteriza uma detecção de movimento no vídeo._**

	**_Apesar de simples e eficiente, esse método possui algumas desvantagens quando aplicado no mundo real. Essa técnica é bastante penalizada, devido às mudanças do ambiente, como sombras, reflexos, variação da posição da câmera, tudo que é passível de alterar o background adotado. Caso isso ocorra haverá uma falsa detecção de movimentação, uma vez que essas mudanças do ambiente não caracterizam um objeto em movimento._**

	**_Então, para utilizar-se dessa técnica de forma satisfatória, sistemas baseados em background subtraction/foreground detection devem operar em ambientes com iluminação controlada e com câmera fixa na posição de atuação._**



---
4. [**Projeto Github**, 2016] - [**Speedtrack** - Python + OpenCV tool to count cars on the road in front of my house](https://github.com/iandees/speedtrack)

	>"Capture a frame of RGB video from the webcam. Convert it to HSV and pick out only the Value channel to convert to grayscale. After converting to grayscale, apply a blur function and add the frame to the running average of the scene."

	>**Prior Art and Helpful Information**
	>- Kyle Hounslow has an excellent set of YouTube tutorials on OpenCV. His [tutorial on Method of Sequential Images](https://www.youtube.com/watch?v=X6rPdRZzgjg) was a big help in getting started.  
	>- Claude Paeau's [YouTube video](https://www.youtube.com/watch?v=eRi50BbJUro) on motion tracking in his front yard was what got me started down this road. His code walkthrough helped me get started.

![4](https://cloud.githubusercontent.com/assets/261584/15658331/2cd1615e-2689-11e6-8dcf-2cc9184a01f6.png)

---
5. [**Projeto Github**, atualizado] - [SPEED CAMERA - Object Motion Tracker](https://github.com/pageauc/speed-camera)  
**[11/07/18 - Broch] _- Parece bem interessante, dar uma olhada e tentar rodar o que já está feito. Pode rodar em Raspberry Pi, então não exige muito poder computacional_**

	>RPI, Unix and Windows Speed Camera Using python, openCV, USB Cam or RPI camera module

	>**Program Description**  
	>- This is a raspberry pi, **Windows, Unix** Distro computer **openCV** object speed camera demo program. It is written in **Python** and uses openCV to **detect and track the x,y coordinates of the largest moving object in the camera view** above a minimum pixel area.  

---
6. [**Projeto Github**, 2014] - [Motion-detection-OpenCV](https://github.com/RobinDavid/Motion-detection-OpenCV)  
**[13/07/18 - Broch] _- É apenas 2 códigos em Python que utilizam Motion-detection_**

	>**The simple way**
	>- The trivial idea is to compute the difference between two frames apply a threshold the separate pixels that have changed from the others and then count all the black pixels. Then the average is calculated with this count and the total number of pixels and depending of the ceil the event is triggered or not.

7. [**Projeto Github**, 2016] - [Vehicle Detection with Haar Cascades](https://github.com/andrewssobral/vehicle_detection_haarcascades)  
**[25/07/18 - Broch] _- Tem que testar, como utiliza Haar Cascades. Dá pra treinar um dataset específico (Tem uns links de outros projetos, ensinando como treinar para gerar os arquivo .xml)._**    
**[25/07/18 - Broch] _- Talvez utilizando as Haar Features resolva em partes aquele problemas causados com oclusão de carros, sombras e iluminação._**

---
# [VI - Tutoriais e Projetos que não são específicos para detecção de velocidade](#conteúdo)


1. [Tutorial, 2017] - [Aplicação de visão computacional com OpenCV](https://www.embarcados.com.br/aplicacao-de-visao-computacional-com-opencv/)  
**[13/07/18 - Broch] _- Tem uma parte interessante de como limpar ruído quando a imagem está em preto e branco, mantendo só o ROI._**  
**[13/07/18 - Broch] _- Utiliza OpenCV em C++._**

---
2. [Artigo, 19 pags] - [Detecção automática dos momentos relevantes em vídeos de vigilância veicular](http://www.prpgi.ifba.edu.br/wp-content/uploads/Laionara-Gon%C3%A7alves-de-Ara%C3%BAjo.pdf)  
**[13/07/18 - Broch] _- Tem alguns fluxogramas interessantes_**  
**[13/07/18 - Broch] _- Tem código de detecção de placa_**  

---
3. [Tese, 128 pags, 2013] - [Sistema automático para obtenção de parâmetros do tráfego veicular a partir de imagens de vídeo usando OpenCV](https://1drv.ms/b/s!AhcmkAvgs28vgZwmLmN7UhQvUQ4dAQ)  
**[13/07/18 - Broch] _- Tem uma parte interessante onde explica os FUNDAMENTOS DE VISÃO COMPUTACIONAL_**  
**[13/07/18 - Broch] _- Tem um capítulo destinado à MODELAGEM DO BACKGROUND_**  
**[13/07/18 - Broch] _- Tem um capítulo destinado à SEGMENTAÇÃO DE VEÍCULOS_**

---
4. [TCC, 65 pags, 2012] - [Visão computacional-uma abordagem com software livre](http://bd.centro.iff.edu.br/xmlui/bitstream/handle/123456789/827/VIS%C3%83O%20COMPUTACIONAL.pdf?sequence=1&isAllowed=y)  
**[13/07/18 - Broch] _- Discute um pouco sobre os fundamentos da visão computacional_**  
**[13/07/18 - Broch] _- Utiliza a bib OpenCV Python para resolver um estudo de caso. Também explica um como a biblioteca OpenCV funciona._**  

---
5. [Artigo de Site] - [Uma breve introdução sobre visão computacional](http://diegocavalca.com/uma-breve-introducao-sobre-visao-computacional/)  
**[13/07/18 - Broch] _- Tem uma seção destinado à "Processamento de imagens x Visão computacional" acho interessante discutir um pouco sobre isso, talvez na introdução do TCC._**  

---
6. [Dissertação, 106 págs, 2007] - [Segmentação Fuzzy de Imagens e Vídeos](https://1drv.ms/b/s!AhcmkAvgs28vgZxXouhETH-cHPasrw)  

	> Cap 2 - Segmentação de Imagens.  
	> Cap 3 - Segmentação de Vídeos e **Estimação de Movimento**.  
	> Cap 4 - Segmentação Fuzzy de Imagens.  
	> Cap 5 - Segmentação Fuzzy de Vídeos.  
---
7. [Tutorial, 2015] - [Part 1 - Ball Tracking with OpenCV](https://www.pyimagesearch.com/2015/09/14/ball-tracking-with-opencv/)  
**[25/07/18 - Broch] _- Utiliza OpenCV Python._**  
**[27/07/18 - Broch] _- Tentar rodar o código, tem 120 linhas._**  
![7](https://www.pyimagesearch.com/wp-content/uploads/2015/09/ball-tracking-tails-comparison.jpg)

---
8. [Tutorial, 2015] - [Part 2 - OpenCV Track Object Movement](https://www.pyimagesearch.com/2015/09/21/opencv-track-object-movement/)  
**[25/07/18 - Broch] _- Utiliza OpenCV Python._**  
**[27/07/18 - Broch] _- Tentar rodar o código, tem 160 linhas._**  
![8](https://www.pyimagesearch.com/wp-content/uploads/2015/09/track_object_animated.gif)

---
9. [Tutorial, 2015] - [Simple Vehicle Tracking/Detection System (C++) OpenCV | Windows 10 | x64 | Visual Studio 2015](http://pythonopencv.com/simple-vehicle-trackingdetection-system-c-opencv-windows-10-x64-visual-studio-2015/)  
**[27/07/18 - Broch] _- Utiliza OpenCV C++ talvez seja um problema. Mas o código é bem reduzido, apenas 103 linhas._**  

---
10. [Tutorial, 2017] - [Car tracking with cascades](https://pythonspot.com/car-tracking-with-cascades/)  
**[25/07/18 - Broch] _- Utiliza OpenCV Python e Haar features. Tem os arquivos para serem baixados._**  

---
11. [Tutorial, 2017] - [Vehicle Detection using OpenCV and SVM classifier](http://www.coldvision.io/2017/03/23/vehicle-detection-using-opencv-svm-classifier/)  
**[27/07/18 - Broch] _- Utiliza OpenCV Python e Histogram of Oriented Gradients (HOG). Tem os códigos._**  
![11](http://www.coldvision.io/wp-content/uploads/2017/03/hog_example.png)

---
12. [Tutorial, 2017] - [Tutorial: Making Road Traffic Counting App based on Computer Vision and OpenCV](https://medium.com/machine-learning-world/tutorial-making-road-traffic-counting-app-based-on-computer-vision-and-opencv-166937911660)  
**[27/07/18 - Broch] _- Utiliza OpenCV Python e explica bem como fazer o Tracking._**  
**[27/07/18 - Broch] _- Tem uma parte destinada à aplicação de um filtro depois Background subtraction._**  

![12](https://cdn-images-1.medium.com/max/1200/1*yTW0iqr8QK24Fkb6JJHhLw.png)

---
# [VII - Livros](#conteúdo)

1. [**Livro**, 1999] - [Processamento Digital de Imagem](http://www.ogemarques.com/wp-content/uploads/2014/11/pdi99.pdf)

---	
2. [**Livro**, 56 pags] - [Introdução a Visão Computacional com Python e OpenCV](http://professor.luzerna.ifc.edu.br/ricardo-antonello/wp-content/uploads/sites/8/2017/02/Livro-Introdu%C3%A7%C3%A3o-a-Vis%C3%A3o-Computacional-com-Python-e-OpenCV-1.pdf)  
**[13/07/18 - Broch] _- Basicamente explica como, escreve na imagem, corta, gira, aplica máscara, redimensiona, etc. O bom é que esse livro sempre apresenta um código._**  
**[13/07/18 - Broch] _- Tem um capítulo destinado à "Fatiamento e desenho sobre a imagem"_**  
**[13/07/18 - Broch] _- Tem um capítulo destinado à "Segmentação e métodos de detecção de bordas"_**  
**[13/07/18 - Broch] _- Tem um capítulo destinado à "Identificando e contando objetos"_**  

---
3. [**Livro**, 273 pags] - [OpenCV-Python Tutorials](https://media.readthedocs.org/pdf/opencv-python-tutroals/latest/opencv-python-tutroals.pdf)

---
# [Ver Depois](#conteúdo)

1. [Vehicle Detection with HOG and Linear SVM](https://towardsdatascience.com/vehicles-tracking-with-hog-and-linear-svm-c9f27eaf521a)

2. [LBP cascade for Car detection in Opencv](http://funvision.blogspot.com/2016/12/lbp-cascade-for-car-detection-in-opencv.html)

3. [Coleção dos livros Automate the Boring Stuff with Python](http://inventwithpython.com/)

4. [opencv-tutorial-a-guide-to-learn-opencv/](https://www.pyimagesearch.com/2018/07/19/opencv-tutorial-a-guide-to-learn-opencv/)

5. [Vehicle Detection And Tracking](https://github.com/alexvogel/vehicle-detection-and-tracking)