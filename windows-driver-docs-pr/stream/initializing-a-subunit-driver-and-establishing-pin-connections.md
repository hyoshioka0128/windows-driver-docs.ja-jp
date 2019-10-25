---
title: サブユニット ドライバーの初期化とピン接続の確立
description: サブユニット ドライバーの初期化とピン接続の確立
ms.assetid: 08c7a604-3aa5-4ee0-be55-b58bea0e6df1
keywords:
- Avc 関数ドライバー WDK、サブユニットドライバーの初期化
- Avc 関数ドライバー WDK、pin 接続
- ピン接続 WDK AV/C
- 接続 WDK AV/C
- AV/C サブユニットドライバーの初期化
- pin カウント WDK AV/C
- WDK AV/C の形式
- データ形式 WDK AVStream
- AVCCONNECTINFO
- 外部プラグ接続 WDK AV/C
- KSPIN_DESCRIPTOR
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6a72d381977d6c073bf408a5118fa8402fe8f8d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845571"
---
# <a name="initializing-a-subunit-driver-and-establishing-pin-connections"></a>サブユニット ドライバーの初期化とピン接続の確立


サブユニットドライバーを初期化し、pin 接続を確立するには、次の手順を実行します。

1.  AVC\_関数を送信して[ **\_PIN\_COUNT 要求\_取得**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-get-pin-count)します。 この手順の後続の関数で生成された pin の数を使用して、pin を示します (オフセットの範囲は 0 ~ PinCount-1)。

2.  各 pin について、 [ **\_pin\_記述子要求\_、AVC\_関数**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-get-pin-descriptor)を送信します。 カーネルストリーミング (KS) フィルターの定義を完了するには、avc\_関数と共に渡された、 [**avc\_PIN\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_pin_descriptor)構造体の返された[**KSPIN\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)のメンバーを**取得\_10_ PIN\_記述子**要求。 *Avc*は、kspin\_記述子の**MediumsCount**、**メディア**、データ**フロー**、および**通信**メンバーを入力します。 サブユニットドライバーは、KSPIN\_記述子の構造をコピーし、メンバーをオーバーライドすることを許可されていますが、中程度の一覧はそのままにしておくことをお勧めします (パーマネントサブレベルのプラグ接続用に合成された Guid が一覧に含まれる場合があります)。

    KSPIN\_記述子構造内のポインターは、サブユニットドライバーの物理デバイスオブジェクト (PDO) が削除されるまで残っているページプールを指します。 コンテンツを破棄しないように注意する必要があります。

    サブユニットドライバーは、ポインターがより適した、またはより適切な構造を指している場合、ポインターを置き換えることができます。 ただし、サブユニットドライバーでは、これらのメモリ範囲を解放しないでください。 サブユニットドライバーで (Stream クラスではなく) AVStream が使用されている場合は、 **KsEdit**ルーチンを使用して、このようなメモリ参照を置き換える必要があります。

    *Avc*では、kspin\_記述子の**インターフェイス**、 **DataRanges**、 **Category**、 **Name**、または**ConstrainedDataRanges**の各メンバーは満たさ*れない*ことに注意してください。 サブシステムドライバーでは、これらのメンバーだけでなく、 **IntersectHandler**と省略可能な**コンテキスト**メンバー (手順3で説明します) が、下位フィルタードライバーの*avcstrm .sys*が存在しない場合にも入力します。

    **DataRanges**メンバーのオリジンに関係なく、各標準範囲は、 [**Avcpreconnectinfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avcpreconnectinfo)構造体が追加された (適切な指定子 guid を使用して) 重複する範囲とペアにして、デバイスからコンピューター*への両方をサポートする必要があります。デバイスからデバイスへ*の接続。 *Avc*は、AVC\_関数を介して各ピンの AVCPRECONNECTINFO 構造を提供し、 [ **\_connectinfo 要求\_取得**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-get-connectinfo)できます。

3.  **IntersectHandler**ルーチンは、一致する**DataRanges**構造体の**DataFormat**構造体を作成します。 積集合ルーチンは、AVC\_関数の結果で指定されるか、 **\_記述子を\_取得**したり、サブユニットドライバーによって提供されたりする\_ます。 サブユニットドライバーが独自の交差ハンドラーを提供する場合は、「 [**AV/C Intersect ハンドラー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/nc-avc-pfnavcintersecthandler)」を参照してください。 データの積集合の詳細については、 [AVStream の Datarange 重なり集合](data-range-intersections-in-avstream.md)に関するセクションを参照してください。

    AVCPRECONNECTINFO 範囲に一致する**DataFormat**構造体に[**avcconnectinfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avcconnectinfo)構造体が追加されています。 この構造体は、ローカル pin の AVCPRECONNECTINFO 構造体のコピーであり、**フラグ**メンバーが**hplug**メンバーに置き換えられています。 **Kspin\_フラグ\_AVC\_パーマネント**ビットが設定されている場合、 **Hplug**メンバーは**NULL**のままである必要があります。 **Kspin\_フラグ\_avc\_PCRONLY**または**kspin\_フラグ\_AVC\_Fixedpcr**ビットが**フラグ**に設定されている場合は、 **UnitPlugNumber**とデータ**フロー**のメンバーを使用してを取得します。*61883*の**hplug**ハンドル。 その他のビットの組み合わせ (またはビットなし) は、使用可能な任意のプラグ番号に対して**Hplug**を取得できることを意味します (データ**フロー**メンバーを使用してプラグの方向を決定します)。

    **IntersectHandler**ルーチンは、結果として得られた AVCCONNECTINFO 構造体を*Avc*に渡す必要があります (手順 4. で説明)。 AVCCONNECTINFO を渡すことによって、 *Avc*は後から必要なプラグ接続をユニット内に作成できます (たとえば、ユニット入力または出力プラグとサブユニットの接続先またはソースプラグとの間の接続)。

4.  最後に、データ形式がピンに設定されている場合 (形式ネゴシエーションとデータの交差部分)、pin は AVCCONNECTINFO 構造体の形式を確認する必要があります。 この構造が検出された場合、pin は IEEE 1394 bus との間で、またはコンピューターとの間でデータを移動しません。 代わりに、AVC\_関数を使用して[ **\_connectinfo\_設定**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-set-connectinfo)し、AVCCONNECTINFO の内容を下位のドライバーに送信します。 低いフィルタードライバー ( *Avcstrm .sys*など) と*Avc*ドライバーの両方が接続操作を実行する可能性がありますが、この時点では avcstrm の内容のみがキャッシュされます (接続操作は実行されません)。 下位のドライバーは、提供された AVCCONNECTINFO をキャッシュしません。 このようにして、1つの pin のみが、ユニット間の**Hplug**接続を確立します。 下位フィルタードライバーがない場合は、サブユニットドライバーが AVCCONNECTINFO を下位のドライバーに配信するかどうかを決定する必要があります。 *Avc*は、プラグ制御レジスタ (PCR) のみの接続に対して AVCCONNECTINFO 構造を表示する必要がありません。

    サブユニットが、ストリーム形式の管理に下位フィルタードライバーを使用していない場合、サブユニットドライバーは、IEEE 1394 serial bus プラグ接続を設定します。 詳細については、「 [AV/C ストリーミングの概要](av-c-streaming-overview.md)」を参照してください。

    サブユニットドライバーは、次の場合にピアツーピア接続を設定するために、形式の**Hplug**メンバーをキャッシュする必要があります。

    -   **Hplug**メンバーがサブユニットドライバーによって作成されたものと一致しません。
    -   **DeviceID**メンバーが AVCPRECONNECTINFO でサブユニットドライバーによって受信されたものと一致しません。
    -   データ**フローメンバーが**サブユニットの pin のデータフローと一致しません。

5.  ピン接続リソースを取得する場合は、要求を[**取得\_AVC\_関数**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-acquire)を送信します。 下位のドライバー (またはサブユニットドライバー自体) は、キャッシュされた AVCCONNECTINFO を使用して**Hplug**接続を行います。 サブユニットとユニットプラグ間の内部接続は、キャッシュされた AVCCONNECTINFO を使用して、要求の**取得\_avc\_関数**を受け取ったときに、 *avc*によって行われます。 *Avc*は、内部プラグ制御がない場合、または接続が永続的とマークされている場合に、情報をキャッシュしたり、内部プラグ接続を試行したりしません。

6.  ピン接続リソースを解放する場合は、 [**AVC\_関数\_リリース**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-release)要求を送信します。 下位のドライバーと*Avc*は、キャッシュされた AVCCONNECTINFO を保持します。これにより、代替の*取得*操作と*解放*操作を実行できます。

7.  [**CLR\_connectinfo 構造体\_AVC\_関数**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-clr-connectinfo)を送信して、キャッシュされた AVCCONNECTINFO データを削除します。

**AVC\_関数\_SET\_CONNECTINFO**構造体は、データ共通部分 (ローカル avcconnectinfo) 中に作成される avcconnectinfo 構造体で1回、avcconnectinfo でもう一度呼び出す必要があることに注意してください。形式 (外部 AVCCONNECTINFO) の設定時に渡される構造体。 異なるデバイスのサブユニット間の接続では、フィルタードライバー (たとえば*Avcstrm .sys)* によって外部情報 (外部**hplug**) がキャッシュされ、 *Avc*によってローカル情報がキャッシュされます。 同じデバイス内のサブユニット間の接続の場合、フィルタードライバーは情報をキャッシュしません。また、 *Avc*は外部サブユニットの情報のみをキャッシュします。 フィルタードライバーは、すべての**avc\_関数\_\_CONNECTINFO**要求を*avc*に渡す必要があります。これにより、サブユニットプラグ接続に関する意思決定からもシールドされるようになります。

AV/C 接続ロックビットは、接続時に設定されます。 出力ピン (ソースプラグ) は、オーバーレイ接続を可能にする複数のピンインスタンス (同じ出力から追加の入力へ) を公開します。 ただし、オーバーレイ接続が許可されている場合、*切断*コマンドによって既存のすべての接続が削除されるのを防ぐことはできません。これは、AV/C 仕様に固有のものです。 接続をオーバーレイするときに、サブユニットは複数の**avc\_関数を送信し\_\_CONNECTINFO**関数と**avc\_関数**を設定して、\_を介在させずに要求のペアを取得 **\_リリース**要求)。 さらに、2台目のコンピューターが IEEE 1394 バスに導入された場合や、2つ目の互換性のないアプリケーションが同じコンピューター上で実行されている場合にも、この動作が発生する可能性があります。

AV/C 外部プラグ接続は、 *avc*で直接サポートされていませんが、合成された AVCCONNECTINFO 構造を提供して、サブユニットプラグと外部プラグ間の内部接続を*確立すること*ができます。 サブユニットドライバーは、 [**AVC\_\_関数**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-get-unique-id)を使用して AVCCONNECTINFO 構造体を作成できます。\_一意の\_ID 関数コードを取得して、 **DeviceID**メンバーを入力し、単位アドレス0xff と外部プラグ番号を指定します。**Subunitaddress**メンバーと**SubunitPlugNumber**メンバーに対して、論理 OR 演算子を使用して0x80 と結合されたプラグ番号。データ**フローメンバーで**正しいデータフロー方向を指定します。 **Hplug**メンバーと**UnitPlugNumber**メンバーを**NULL**に設定する必要があります。 入力および出力の外部プラグの数は、AVC\_関数を使用して検出できます。これは、 **\_EXT\_プラグ\_カウント関数\_取得**します。

*Avc*が適切な内部プラグ接続を作成し、可能な外部プラグ接続をアプリケーションに公開できるようにする方法は、可能な外部プラグごとにフィルターファクトリを用意することです。 結果として得られるフィルターインスタンスは、適切な入力ピンまたは出力ピンを公開し、さらに AVCCONNECTINFO 構造体を提供します。

 

 




