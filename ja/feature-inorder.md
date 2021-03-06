## 到着順序の保証

QUICはストリーム内での到着順序を保証しますが、ストリーム間の順序を保証しません。
これは、ストリームは送信したデータの順序を維持しますが、
各ストリームが宛先に到達する順序は
アプリケーションがそれらを送信したときとは異なるものになり得ることを意味します!

たとえば: ストリームAとBはサーバからクライアントに転送されました。
ストリームAは最初に開始され、ストリームBはそれに続きました。
QUICでは、パケットの損失はそのパケットが属する（単独もしくは複数の）ストリーム
にのみ影響を及ぼします。
ストリームAでパケット損失が発生し、ストリームBでは発生しなかった場合、
ストリームAがパケットの再送を行っている間に、ストリームBは転送を継続し、
先に完了するかもしれません。これはHTTP/2では不可能でした。

ここに、2つのQUICエンドポイントが1つのコネクションを介して
黄色のストリームと青色のストリームの転送を行う様子を示す図があります。
それぞれのストリームは独立しており、異なる順序で到達する可能性がありますが、
いずれのストリームも自身の信頼性と到達順序を保証します。

![two QUIC streams between two computers](../images/quic-chain-streams.png)
