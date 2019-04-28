---
title: サブユニット ドライバーの初期化とピン接続の確立
description: サブユニット ドライバーの初期化とピン接続の確立
ms.assetid: 08c7a604-3aa5-4ee0-be55-b58bea0e6df1
keywords:
- Avc.sys 関数ドライバー WDK、サブユニットのドライバーの初期化
- Avc.sys 関数ドライバー WDK、暗証番号 (pin) の接続
- 接続 WDK AV/C をピン留め
- WDK AV/C の接続
- AV/C サブユニット ドライバーの初期化
- pin は、WDK AV/C をカウントします。
- WDK AV/C を書式設定します。
- データ形式の WDK AVStream
- AVCCONNECTINFO
- 外部のプラグイン接続 WDK AV/C
- KSPIN_DESCRIPTOR
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bc66820153027ae747f7b0504bb15614f7c0e19
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360466"
---
# <a name="initializing-a-subunit-driver-and-establishing-pin-connections"></a>サブユニット ドライバーの初期化とピン接続の確立


でサブユニット ドライバーを初期化して、暗証番号 (pin) の接続を確立するには、次の手順を実行します。

1.  送信、 [ **AVC\_関数\_取得\_PIN\_カウント**](https://msdn.microsoft.com/library/windows/hardware/ff554158)要求。 この手順では、後続の関数の結果として得られるピンの数を使用すると、(0 ~ PinCount 1 の範囲をオフセット) の暗証番号 (pin) を指定します。

2.  各ピンには、送信、 [ **AVC\_関数\_取得\_PIN\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff554160)要求。 (KS) フィルターの定義をストリーミングするカーネルを完了するには、するには、返された使用[ **KSPIN\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff563533)のメンバー、 [ **AVC\_暗証番号(pin)\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff554185)で渡された構造体、 **AVC\_関数\_取得\_PIN\_記述子**要求。 *Avc.sys*塗りつぶす、 **MediumsCount**、**メディア**、**データフロー**、および**通信**KSPINのメンバー\_記述子。 サブユニット ドライバーのコピー、KSPIN で許可されている\_記述子構造体であり (一覧は、合成の永続的なサブユニット プラグ接続 Guid を含む可能性があります)、そのままから中程度リストのままにして、ことをお勧めしますが、メンバーのオーバーライド.

    KSPIN ポインター\_サブユニット ドライバーの物理デバイス オブジェクト (PDO) が削除されるまでに残っているページのプールに記述子構造体のポイント。 内容を破棄するように注意する必要があります。

    指す、またはより適していますが、構造がある場合は、ポインターを置換するサブユニット ドライバーが許可されます。 ただし、サブユニット ドライバーは、これらのメモリ範囲を解放する必要があります。 サブユニット ドライバー (Stream クラスにある) ではなく AVStream を使用するかどうかは、どちらを使用する、 **KsEdit**ルーチンをこのようなメモリ参照に置き換えます。

    なお*Avc.sys*は*いない*、KSPIN 入力\_記述子の**インターフェイス**、 **DataRanges**、 **カテゴリ**、**名前**、または**ConstrainedDataRanges**メンバー。 サブユニット ドライバーは、これらのメンバーに格納だけでなく**IntersectHandler**と省略可能な**コンテキスト**メンバー (手順 3. で説明されている) 場合、低いフィルター ドライバー *Avcstrm.sys*が存在しません。

    配信元に関係なく、 **DataRanges** 、メンバーが重複する範囲で、それぞれの標準的な範囲を組み合わせる必要があります、 [ **AVCPRECONNECTINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff554103)構造追加時 (で適切な指定子の Guid を使用して) 両方デバイスのコンピューターをサポートするために*と*デバイスからデバイスへの接続。 *Avc.sys*を通じて各ピンの AVCPRECONNECTINFO 構造体を指定することができます、 [ **AVC\_関数\_取得\_接続情報**](https://msdn.microsoft.com/library/windows/hardware/ff554154)要求。

3.  **IntersectHandler**ルーチンを作成し、 **DataFormat**の一致するペアの構造**DataRanges**構造体。 積集合ルーチンがの結果で指定されたか、 **AVC\_関数\_取得\_暗証番号 (pin)\_記述子**サブユニット ドライバーによって提供されるか。 サブユニット ドライバーでは、独自の積集合のハンドラーを提供する場合は、次を参照してください。 [ **AV/C 交差ハンドラー**](https://msdn.microsoft.com/library/windows/hardware/ff556379)します。 データの交差部分の詳細については、次を参照してください。 [AVStream の交差部分を DataRange](data-range-intersections-in-avstream.md)します。

    **DataFormat**が AVCPRECONNECTINFO 範囲に一致する構造体、 [ **AVCCONNECTINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff554101)構造が追加されます。 この構造体をローカルの pin の AVCPRECONNECTINFO 構造体のコピーである、**フラグ**メンバーに置き換え、 **hPlug**メンバー。 **HPlug**メンバーである必要があります**NULL**場合、 **KSPIN\_フラグ\_AVC\_永続的な**ビットが設定されます。 場合、 **KSPIN\_フラグ\_AVC\_PCRONLY**または**KSPIN\_フラグ\_AVC\_FIXEDPCR** で設定されたビット**フラグ**、 **UnitPlugNumber**と**データフロー**取得に使用されるメンバー、 **hPlug**から処理*61883 します。sys*します。 ビット (またはないビット) の他の任意の組み合わせ。 つまり、 **hPlug**使用可能なプラグインの任意の数を取得することができます (を使用して、**データフロー**プラグの方向を判断するにはメンバー)。

    **IntersectHandler**ルーチンは、下に結果として得られる AVCCONNECTINFO 構造体を渡す必要があります*Avc.sys* (手順 4 で説明)。 確実に渡す AVCCONNECTINFO *Avc.sys*後自体 (たとえば、単位入力またはサブユニットの宛先にプラグインするときに出力プラグインするときにソース間の接続) を単位内のすべてのプラグインが必要な接続を行うことができます。

4.  最後に、(形式のネゴシエーションとデータの交点) した後、暗証番号 (pin) のデータ形式を設定すると、pin は AVCCONNECTINFO 構造体の形式を調べる必要があります。 この構造体が見つかると、pin からの IEEE 1394 bus との間、またはコンピューターに、データを移動されません。 代わりに、使用[ **AVC\_関数\_設定\_接続情報**](https://msdn.microsoft.com/library/windows/hardware/ff554171) AVCCONNECTINFO 内容を下位のドライバーに送信します。 場合によっては、両方、低いフィルター ドライバー (たとえば、 *Avcstrm.sys*) および*Avc.sys*ドライバー接続操作を実行するが、この時点では、AVCCONNECTINFO 内容のみがキャッシュされている (をする必要があります接続操作では実行されません)。 下位のドライバーを提供している AVCCONNECTINFO をキャッシュしません。 1 つだけの pin では、この方法で**hPlug**ユニット間の接続。 低いフィルター ドライバーがない場合は、サブユニット ドライバーは、AVCCONNECTINFO を下位のドライバーに配信するかどうかを決定する必要があります。 *Avc.sys*必要があるプラグの AVCCONNECTINFO 構造を表示するコントロールを登録しません (PCR) の接続のみです。

    サブユニットは stream の形式を管理する低いフィルター ドライバーが使用していない場合、サブユニット ドライバーは、IEEE 1394 シリアル バス プラグの接続を設定します。 詳細については、次を参照してください。 [/C AV ストリーミングの概要](av-c-streaming-overview.md)します。

    サブユニット ドライバーをキャッシュする必要があります、 **hPlug**場合、ピア ツー ピア接続をセットアップする形式のメンバー。

    -   **HPlug**メンバーは、サブユニット ドライバーによって作成されたものと一致しません。
    -   **DeviceID**メンバーは、サブユニットのドライバーを AVCPRECONNECTINFO で受信した 1 つと一致しません。
    -   **データフロー**メンバーは、サブユニットの暗証番号 (pin) のデータ フローと一致しません。

5.  暗証番号 (pin) の接続リソースは、取得するのには、送信、 [ **AVC\_関数\_ACQUIRE** ](https://msdn.microsoft.com/library/windows/hardware/ff554148)要求。 下位のドライバー (または自身のサブユニット ドライバー) を使用して、キャッシュされた AVCCONNECTINFO、 **hPlug**接続します。 サブユニットおよび単位のプラグ間の内部接続がによって行われた*Avc.sys*受信すると、 **AVC\_関数\_取得**要求と、キャッシュされた AVCCONNECTINFO を使用します。 *Avc.sys*は情報をキャッシュも試行内部プラグイン接続内部プラグイン コントロールがない場合や、接続は的なものとしてマークされている場合。

6.  暗証番号 (pin) の接続リソースは、解放するのには、送信、 [ **AVC\_関数\_リリース**](https://msdn.microsoft.com/library/windows/hardware/ff554169)要求。 下位のドライバーと*Avc.sys*ように、キャッシュされた AVCCONNECTINFO 交互*取得*と*リリース*操作を実行できます。

7.  送信、 [ **AVC\_関数\_CLR\_接続情報**](https://msdn.microsoft.com/library/windows/hardware/ff554149) AVCCONNECTINFO のキャッシュされたデータを削除する構造体。

なお、 **AVC\_関数\_設定\_接続情報**構造体は、データの交差部分 (ローカル AVCCONNECTINFO) 中に作成された AVCCONNECTINFO 構造で 1 回呼び出す必要があり、もう一度ときに渡される AVCCONNECTINFO 構造を持つには、(外部 AVCCONNECTINFO) の形式を設定します。 サブユニット フィルター ドライバーのさまざまなデバイスの間の接続 (たとえば、 *Avcstrm.sys)* 外部の情報をキャッシュ (外部**hPlug**)、および*Avc.sys*ローカル情報をキャッシュします。 同じデバイス内のサブユニットの間で接続の場合、フィルター ドライバーをキャッシュしませんの情報と*Avc.sys*外部のサブユニットの情報のみをキャッシュします。 フィルター ドライバーは、すべてを渡す必要があります**AVC\_関数\_設定\_接続情報**下に要求*Avc.sys*に関する意思決定をシールドすることができるように、サブユニットは、接続を接続します。

接続するときに、AV/C 接続のロックのビットが設定されています。 (ソースの接続) の出力ピンは、(同じ出力に追加の入力) からのオーバーレイの接続を許可する複数の暗証番号 (pin) のインスタンスを公開します。 ただし、オーバーレイの接続が許可されている場合何もできないように、*切断*コマンドからのすべての既存の接続を削除しています。 これには、AV/C 仕様に固有です。 接続をオーバーレイのサブユニットを複数送信**AVC\_関数\_設定\_接続情報**と**AVC\_関数\_の取得**のペアを要求 (の介在なし**AVC\_関数\_リリース**要求)。 さらに、2 番目のコンピューターが IEEE 1394 バスに導入された、または同じコンピューターで 2 つ目の互換性のないアプリケーションを実行時に、これと同じ動作が発生することができます。

AV/C プラグの外部接続がによって直接サポートされていない*Avc.sys*が*Avc.sys*提供することでサブユニット プラグと外部プラグ間の内部接続を確立できますも合成AVCCONNECTINFO 構造体。 サブユニット ドライバーを使用して AVCCONNECTINFO 構造体を作成することができます、 [ **AVC\_関数\_取得\_UNIQUE\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff554166)関数コードを入力するには**DeviceID**単位アドレス 0 xff までを提供して、メンバーと外部の番号 (番号のプラグに論理 OR 演算子を使用して、0x80 に参加させる) を接続、 **SubunitAddress**と**SubunitPlugNumber**メンバーと適切なデータを提供するフロー方向、**データフロー**メンバー。 **HPlug**と**UnitPlugNumber**にメンバーを設定する必要があります**NULL**します。 によって外部プラグが入力と出力の数を検出できる場合、 **AVC\_関数\_取得\_EXT\_プラグ\_カウント**関数。

許可する手法*Avc.sys*アプリケーションへの接続が可能な各外部プラグインのフィルター ファクトリには、適切な内部のプラグイン接続および公開可能な外部プラグをします。 結果として得られるフィルター インスタンスは、適切な入力または出力ピンは、さらに AVCCONNECTINFO 構造体を提供を公開します。

 

 




