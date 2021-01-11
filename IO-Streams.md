# I/O Streams

Byte Streams: 8ビットの入出力
├InputStream
│├FileInputStream
│└...
└OutputStream
 ├FileOutputStream
 ├PrintStream: フォーマットを実装している（System.out, System.err）
 └...

Character Streams: ローカルの文字セットの入出力
├Reader
│├FileReader: 物理I/OにFileInputStreamを使用
│└...
└Writer
 ├FileWriter: 物理I/OにFileOutputStreamを使用
 ├PrintWriter: フォーマットを実装している
 └...

general-purpose byte-to-character "bridge" streams: 目的に合致する、あらかじめパッケージされたcharacter streamsがない時にcharacter streamsを作成する時に使う
├InputStreamReader
└OutputStreamWriter

Buffered Streams: バッファーを利用していないstreamsをwrapする
├Input
│├BufferedInputStream
││└InputStream
│└BufferedReader
│ └Reader
└Output
 ├BufferedOutputStream
 │└OutputStream
 └BufferedWriter
  └Writer

I/O from the Command Line
├Standard Streams
│├Standard Input: System.in
│├Standard Output: System.out
│└Standard Error: System.err
└Console
