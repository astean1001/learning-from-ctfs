BITSCTF 2017
=======

1. HEX, ELF 
<br><br>리버싱 20점 짜리 문제인 Mission Improbable은 정말로 쉬운 문제였음에도 불구하고 풀지 못했는데, 그 이유라고 하면 내가 HEX가 정확히 어떤 파일인지 몰랐기 때문에 힌트에 있는 USB Rubber Ducky를 따라서 <a href="https://github.com/hak5darren/USB-Rubber-Ducky"> 어떤 Github 페이지</a>로 가서 삽질을 했기 때문이다.<br>
그냥 헥스 에디터로 열어서는 어떤 파일인지 전혀 몰랐다. Hex 파일은 다음과 같은 <a href="http://crasy.tistory.com/79">xxd 명령어</a>를 통해서 ELF형식의 실행 파일로 돌려놓을 수 있다는 모양이다.
<pre> xxd -r -p MissionImprobable.TEENSY31.hex out</pre>

2. file, strings 명령어
<br><br>일단 대부분의 리버싱이나 포렌식, 기타 문제들은 그 파일이 어떤 파일인지 규명하는 것이 중요해 보인다. 기존에는 항상 HEX 에디터로 열어보고 헤더에 있는 키워드를 통해 파일 형식을 파악했는데, ELF의 경우 file을 통해서 개략적으로 어떤 환경의 실행 파일인지 알아볼 수 있다. strings는 파일을 적절히 ASC II형태로 변환해서 보여주는데, 이는 생각 이상으로 도움이 되는 모양이다.

3. ROT13
<br><br>깨진 PDF 파일을 복원 하는 문제였던 Banana Princess에서 사용된 암호화 체계라고 한다. Ceasar Cipher 중에서 13번 민 것을 부르는 말이라고 한다. 딱히 나중에 쓰이거나 할 것 같지는 않지만 유래가 특이하고 시저 사이퍼 중에서 이름이 있는 녀석이라 한번 기록해 보았다.

4. Base32 그리고 Affine Cipher
<br><br>Base32키를 복호화하는 문제에서 사용되는 것이 Affine Cipher인데, (ax + b) mod m의 방식 (a와 b는 암호화 키, m은 사용되는 글자의 갯수)로 암호화하는 방법이라고 한다. a가 1이면 시저 사이퍼가된다. Base32의 한 암호화 블럭이 5bit라는 사실과 KEY의 시작부분이 BITSCTF{로 시작한다는 것을 알면 쉽게 풀수 있는 문제였다. <a herf="http://www.herongyang.com/Encoding/Base32-Encoding-Algorithm.html">Base32의 인코딩 알고리즘</a>에 대해서 자세히 알아보는 것도 좋을 것 같다. 이 문제를 풀 때, 시저 사이퍼 계통일 것이라고 예상해서 시저 사이퍼를 돌렸지만 실패했던 이유가 시저 사이퍼가 아닌 어파인 사이퍼였기 때문이었다는 점이 아쉽다.

5. XOR 암호화
<br><br>암호 문제중 두 문제가 XOR 암호화에 관한 문제였는데, <a href="https://wiremask.eu/tools/xor-cracker/">Wireshark의 프로그램</a>을 이용하면 쉽게 풀린다는 점이 매우 웃기다. 다만, XOR을 직접 푸는 방법을 알 필요가 있다는 점은 중요하다.

6. PCAP 데이터들...
<br><br>대회 기간 내내 나를 제일 괴롭혔던 것들 중의 하나는 pcap 데이터들이었다. 와콤 펜 데이터(패킷에 남은 데이터가 펜의 이동 좌표였다.)부터 시작해서, 키보드에서 전송되어 오는 데이터 (컴퓨터에서 쏘는 캡스 락 가동 신호를 통해 키보드의 LED를 통해 모스 코드를 송신한 흔적이라고 한다.), 처음보는 DC++/ADC 프로토콜? 까지...... 일단 패킷의 정체와 용도, 명세에 대해 알아 보는 것이 상당히 중요하다고 생각한다. 파일에 있는 Flag를 꺼내는 문제는 실제로 거의 다 풀었는데 타이거 트리 해시에 있는 값을 꺼내지 못해서 망해버렸다.

7. Pwnable
<br><br>나 정말 포너블은 아예 손을 못댄다. 기초부터 공부할 필요가 있겠다.
