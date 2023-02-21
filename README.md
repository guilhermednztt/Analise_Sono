<h1 align="center">:zzz:<br>Análise de Sono</h1>

<b>O algoritmo:</b> o algoritmo visa capturar frames de um rosto e tenta identificar se a pessoa está dormindo ou não, de forma rápida (em tempo real). Para inferir o estado de sono em uma pessoa foi levado em consideração alguns parâmetros:
<u>
<li><b>Abertura dos Olhos:</b> dos 468 pontos faciais identificados pela lib MediaPipe, 12 são nos olhos (6 em cada). Os pontos são posicionados na mesma linha dos cílios e acompanham os movimentos de abrir e fechar dos olhos. Com isso, foi calculado a distância euclidiana entre esses pontos para descobrir seus níveis de proximidade e perceber quando o olhou fechou ou abriu.<br>
<br><p align="center"><img src="https://user-images.githubusercontent.com/121525620/220442839-976a834d-80b7-4339-aa23-d74ad2c7925c.png" width="300" height="100"></p>
</li>
<li><b>Abertura da Boca:</b> em um processo semelhante ao dos olhos, porém com 8 pontos identificados. Os pontos seguem a linha inferior dos lábios e por essa razão, mesmo sorrindo não significa que abriu a boca, pois os lábios podem estar juntos durante o sorriso.<br>
<br><p align="center"><img src="https://cdn1.gnarususercontent.com.br/1/563691/e5570834-3b57-4ed0-b0bc-2324a32cdefc.png" width="300" height="150"></p></li>
<li><b>Quantidade de Piscadas:</b> existe uma relação direta entre o nível do sono e a quantidade de piscar de olhos por minuto, por isso a cada vez que o olho fecha é considerado 1 piscar a mais para saber se a quantidade está satisfatória ou se apresenta forte sobrecarga de sono.</li>
<br><li><b>Tempo:</b> a partir do momento que o olho e/ou a boca se fecham, inicia a contagem. Caso os olhos e a boca permaneçam fechados por 1.5 segundo, considera-se estado de sono e é exibido uma mensagem na tela "Dormindo!" para mostrar que identificou a sonolência.</li>
</u>

<br><br>
<b>Cálculos:</b> a fórmula aplicada para calcular os dois primeiros itens acima são da seguinte forma:

| Olhos | Boca |
|--- |--- |
| <img src="https://user-images.githubusercontent.com/121525620/220448363-c86a5d94-b614-4509-94e0-9b963e6b743e.png"> | <img src="https://user-images.githubusercontent.com/121525620/220448526-2166ddda-179b-422e-b9fe-cce64a7ffc92.png"> |



<br>
Os parâmetros são calculados continuamente, enquanto a captura identifica os pontos faciais, e exibe na visualização das imagens conforme é mostrado abaixo:<br>

<p align="center"><img src="https://user-images.githubusercontent.com/121525620/220444303-4c956336-7e1b-4dae-8018-46aa7aa02f39.png"></p>
<br>

| Parâmetros | Descrição |
|--- |--- |
| EAR | Eye Aspect Ratio - valor médio da distância euclidiana entre todos os pontos dos olhos. |
| MAR | Mouth Aspect Ratio - valor da distância euclidiana entre todos os pontos da boca. |
| TIME | Contagem de tempo em que a boca e os olhos permanecem fechados, em segundos. |
| BLINKS | Contagem do piscar de olhos, valor apenas incremental. |
| BLINKS /MIN | Quantidade de piscar de olhos no último minuto. Esse valor, por sua vez, atualiza a cada 60 segundos sendo possível que já tenha registrado uma altíssima quantidade de piscada, mas no último minuto a quantidade pode ser bem pequena. |

Quando os parâmetros estão dentro dos limiares do que é considerado estado de sonolência (EAR = 0.17, MAR = 0.11, TIME = 1.5, BLINKS /MIN < 10), o algoritmo exibe a mensagem de que identificou o sono:
<p align="center"><img src="https://user-images.githubusercontent.com/121525620/220447427-338fb558-00c9-479c-a993-66dbe5852bb5.png"></p>

<br><br>
<p align="center"><b>Python, MediaPipe, OpenCV, NumPy, Visão Computacional</b><br>Guilherme Donizetti</p>
