---
Description: In this topic, you will learn about the chained MDLs capability in the USB driver stack, and how a client driver can send a transfer buffer as a chain of MDL structure.
title: チェーンされた MDLs を送信する方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e9ffe07dbb30ff43144ace3f621dd55ae766265
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538511"
---
# <a name="how-to-send-chained-mdls"></a>チェーンされた MDLs を送信する方法


このトピックでは、USB ドライバー スタック、およびクライアント ドライバーがのチェーンとして転送バッファーを送信する方法では、チェーンの MDLs 機能について学習[ **MDL** ](https://msdn.microsoft.com/library/windows/hardware/ff554414)構造体。

ほとんどの USB ホスト コント ローラーには、実質的に連続して転送バッファーが必要です。 連続する事実上は、バッファーの開始し、ページがバッファーの残りの部分で任意の場所を終了できることを意味する必要があります起動し、ページの境界で終了します。 多くの USB クライアント ドライバーでは、その要件を満たすことができます。 ただし、特定のクライアント ドライバーが特に必要とする内容を追加または削除するか、バッファーから追加のデータの転送バッファーのほぼ連続したメモリの割り当てはことをお勧めします。

たとえば、次の 3 つのドライバー、ネットワーク プロトコルのドライバー、中間ドライバーでは、およびミニポート ドライバーのネットワーク スタックを検討してください。 プロトコル ドライバーの転送を開始して、スタック内の次のドライバーにパケットを送信します。 中間ドライバー。 中間のドライバーは、パケットにカスタム ヘッダー (メモリの個別ブロックに含まれる) を追加する場合します。 中間ドライバー ヘッダーと、受信したパケットの場合をスタック内の次のドライバーに送信されます: ミニポート ドライバー。 ミニポート ドライバーでは、USB ドライバー スタックとのインターフェイスし、そのため、実質的に連続する転送バッファーを準備する必要があります。 そのようなバッファーを作成するには、ミニポート ドライバーは、大きなバッファーを割り当てます。 カスタム ヘッダーを追加し、ペイロードをコピーします。 ペイロードは通常、大規模なため、ペイロード全体をコピーすると、パフォーマンスに大きな影響があります。

クライアント ドライバーのチェーンとして転送バッファーを送信してそのパフォーマンスに与える影響を克服できます*メモリ記述子のリスト*(MDLs)。 Windows 8 の新しい USB ドライバー スタックは連鎖 MDL を受信できる (を参照してください[ **MDL**](https://msdn.microsoft.com/library/windows/hardware/ff554414))、クライアント ドライバーから。 クライアント ドライバーは連鎖 MDL を指定することによって、余分なコピー操作を実行する代わりに、メモリ内の不連続のページを参照できます。 機能は、数、サイズ、および物理メモリのセグメント化の転送バッファーの許可、バッファーの配置に関する制約を削除します。

連鎖 MDLs を使用するにはクライアント ドライバーは、Windows によって読み込まれる、基になる USB ドライバー スタックは、機能をサポートするかどうかを検出し、MDLs の適切な順序でのチェーンを構築しする必要があります。

### <a name="prerequisites"></a>前提条件

連鎖 MDL 機能は一括でアイソクロナス、のみサポートされており、割り込みを転送します。 連鎖 MDL 機能のクエリを実行する前に、クライアント ドライバーがドライバーの登録は USB ドライバー スタックと USBD ハンドルを確認します。 USBD ハンドルを作成するには[ **USBD\_CreateHandle**](https://msdn.microsoft.com/library/windows/hardware/hh406241)します。通常、クライアント ドライバーは USBD のハンドルを作成します。 その[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチン。

クライアント ドライバーの連鎖 MDL 機能を照会できます[ **IRP\_MN\_開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551749)ハンドラーまたはそれ以降いつでもできます。 クライアント ドライバーかでこの機能を照会する必要があります、 [ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチン。

<a name="instructions"></a>手順
------------

1.  呼び出す、 [ **USBD\_QueryUsbCapability** ](https://msdn.microsoft.com/library/windows/hardware/hh406230)ルーチンを USB ドライバー スタックが連鎖 MDLs 機能をサポートするかどうかを確認します。 その機能を照会するには、GUID として UsbCapabilityChainedMdls を指定します。 設定、 *OutputBuffer*パラメーターを NULL と*OutputBufferSize*パラメーターを 0 にします。
2.  によって返される NTSTATUS 値をチェックして[ **USBD\_QueryUsbCapability** ](https://msdn.microsoft.com/library/windows/hardware/hh406230)し、結果を評価します。 ルーチンが正常に完了すると、連鎖 MDLs 機能はサポートされています。 その他の値は、機能がサポートされていないことを示します。
3.  MDLs のチェーンを作成します。 各[ **MDL** ](https://msdn.microsoft.com/library/windows/hardware/ff554414)が、**次**別を指すポインター **MDL**します。

    手動で設定して、ドライバーが MDL のチェーンの構築、**次**ポインター。

    前の例では、プロトコル ドライバーには、MDL として、パケットを送信します。 中間のドライバーを作成[ **MDL** ](https://msdn.microsoft.com/library/windows/hardware/ff554414)ヘッダー データを使用してメモリのブロックを参照します。 チェーンを作成する中間のドライバーがヘッダー MDL をポイントできます**次**プロトコル ドライバーから受信した MDL へのポインター。 中間のドライバーは、ミニポート ドライバーで要求の URB 連鎖 MDL への参照を提供し、USB ドライバー スタックに要求を送信する 2 つの MDLs のチェーンを転送できます。 詳細については、次を参照してください。[を使用して MDLs](https://msdn.microsoft.com/library/windows/hardware/ff565421)します。

4.  設定を使用する I/O 要求チェーン MDLs 向け、URB の作成に、中に、 **TransferBufferMDL** 、関連付けられているメンバー [ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)構造 (など[ **\_URB\_一括\_OR\_INTERRUPT\_転送**](https://msdn.microsoft.com/library/windows/hardware/ff540352)または[  **\_URB\_アイソクロナス\_転送**](https://msdn.microsoft.com/library/windows/hardware/ff540414)) にチェーン、およびセットの最初の MDL、 **TransferBufferLength**に転送するバイトの合計数。 データは、MDL チェーン内の 1 つ以上の MDL エントリにまたがる可能性があります。

    Windows 8 で 2 つの新しい種類の URB 関数が追加されましたデータ転送のチェーン MDLs を使用するクライアント ドライバーを有効にします。 この機能を使用する場合は、設定されていることを確認する、**関数**URB ヘッダーのメンバー URB 関数を次のいずれかに設定されます。

    -   URB\_関数\_一括\_または\_INTERRUPT\_転送\_USING\_連結された\_MDL
    -   URB\_関数\_アイソクロナス\_転送\_USING\_連結された\_MDL

    これらの URB 関数については、次を参照してください。 [  **\_URB\_ヘッダー**](https://msdn.microsoft.com/library/windows/hardware/ff540409)します。

<a name="remarks"></a>注釈
-------

ドライバー スタックが連鎖 MDLs を受け入れるかどうかを判断する基礎となる USB ドライバー スタックのクエリを実行するコード例では、次を参照してください。 [ **USBD\_QueryUsbCapability**](https://msdn.microsoft.com/library/windows/hardware/hh406230)します。

## <a name="related-topics"></a>関連トピック
[USB I/O 操作](usb-device-i-o.md)  



