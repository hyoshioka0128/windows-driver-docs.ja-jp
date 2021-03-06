---
title: ピア サブユニット ドライバー スタック
description: ピア サブユニット ドライバー スタック
ms.assetid: 6ef4b6ae-3802-4ba9-acfa-4b3edba11ba3
keywords:
- ピアのサブユニット ドライバー WDK AV/C をスタックします。
- ドライバーは、WDK AV/C をスタックします。
- WDK AV/C のスタック
- サブユニット サポート WDK AV/C
- AV/C WDK、ドライバー スタック
- 単位は、WDK AV/C をコマンドします。
- 組み込みの拡張機能メカニズム WDK AV/C
- コマンド拡張機能メカニズム WDK AV/C
- コマンドの対象 WDK AV/C
- Avc.sys 関数ドライバー WDK、ドライバー スタック
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76de7fb53b1746c02a294ab539c03fb175df0b5f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370375"
---
# <a name="peer-subunit-driver-stack"></a>ピア サブユニット ドライバー スタック


ピアのドライバー スタックは、コンピューターから制御できるし、IEEE 1394 バス上でアクティブになっている AV/C サブユニットを表すために読み込まれるドライバーで構成されます。 AV/C ピア ドライバー スタックを通じた外部デバイスの制御を開始する必要があります。 Windows のインスタンスを読み込みます*Avc.sys*デバイスとは、システムに接続されている (またはシステムの起動中に存在) されるたびに、IEEE 1394 バス上の外部 AV/C デバイスごとにします。 各インスタンス*Avc.sys*はピアのサブユニット ドライバー登録 GUID の新しいインスタンスをサポートするために読み込まれた\_AVC\_クラス デバイスのインターフェイス。 GUID の詳細については\_AVC\_デバイス インターフェイスのクラスを参照してください[を使用して Avc.sys](using-avc-sys.md)と[ **IOCTL\_AVC\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ni-avc-ioctl_avc_class).

ピアのサブユニット ドライバーに対するアクセスし、制御を通じて、IOCTL 委譲\_AVC\_によってエクスポートされるクラス インターフェイス*Avc.sys*します。 *Avc.sys* IEC 61883 関数制御プロトコル (FCP) でのすべての操作を含む、AV C/コマンド/応答プロトコルを処理します。 ただし、ピアのサブユニット ドライバーがないので注意できなくとの通信および特定に直接アクセスする*61883.sys*必要な場合に機能します。 サブユニット ドライバーと直接通信する必要があります*61883.sys*サブユニット ドライバーが Microsoft をサポートしないストリームの形式を使用する AV/C サブユニットを表す場合。 サブユニット ドライバーを使用して、 **IOCTL\_61883\_クラス**と直接通信できるインターフェイス*61883.sys*必要な場合。 Microsoft は、低いフィルター ドライバーを提供*Avcstrm.sys*DV をストリーミングする役に立つ、MPEG2 書式設定します。 詳細については*Avcstrm.sys*を参照してください[/C AV ストリーミングの概要](av-c-streaming-overview.md)します。

ユーザーに通知され、AV/C の外部デバイスからの AV/C コマンドを受信するピアのサブユニット ドライバーを登録できます。 ピアのサブユニット ドライバーの問題を登録する、 [ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control) でI/O要求パケット(IRP)**IoControlCode**の IOCTL メンバー\_AVC\_クラス I/O 制御コードとサブ機能は、AVC に設定\_関数\_取得\_を要求します。 この機能は、ピアは、サブユニットのドライバーのサブユニットから AV/C 要求を受信し、接続と互換性の管理 (CCM) のプロトコルやデジタル コンテンツの転送の保護 (DTCP) などの仕様のサポートを有効に. 詳細については、CCM は、次を参照してください。、 [IEEE 1394 貿易](https://go.microsoft.com/fwlink/p/?LinkId=518448)web サイト。 DTCP の詳細については、次を参照してください。、[伝送のデジタル ライセンス管理者](https://go.microsoft.com/fwlink/p/?linkid=8731)web サイト。

この機能が仮想 AV/C サブユニット ドライバー (サブユニット ドライバーは、仮想の AV/C デバイス スタックである)、コンピューターに AV/C コマンドを送信して、AV/C コマンドを送信する外部デバイス上の AV/C のサブユニットを許可をサポートするものであるに注意してください、コンピューター システム。

### <a href="" id="peer-stack-as-av-c-command-target"></a>**AV/C コマンド ターゲットとしてのピア スタック**

ピアのサブユニット ドライバー スタックは、ベンダー固有またはデバイスに固有のターゲット AV/C の機能を提供する追加の WDM フィルター ドライバーを含めることができます。 このピアのサブユニット ドライバー スタックの拡張機能メカニズムにより、サード パーティ ベンダー個別に実装できますしない Microsoft によって提供される AV/C 実装の拡張機能と同様に、コピー防止を 5 C などの付加価値機能。

サブユニット ドライバーはこの関数を実行できますが、複数のサブユニットでデバイス、WDM フィルター ドライバーは、推奨される方法。 上のドライバー (ドライバーのサブユニットまたはフィルター) を経由の着信要求を受信登録する場合は、コンピューター、AV/C をターゲットとして公開のみ[ **AVC\_関数\_取得\_要求**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-get-request). AV/C 単体のコマンドの詳細については、次を参照してください。 [ **AVC\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ne-avc-_tagavc_function)します。

デバイス識別子 (Id) に基づくドライバーの読み込みそのため、単体の機能を選択的に読み込む特定のデバイスまたはベンダー固有の単位でできます。 一般的に、仮想のサブユニット ドライバー スタックにこのメカニズムがサポートしています (デバイス固有の方法) ではないです。

デバイス固有の単位の拡張機能、任意のハンドルされない単位コマンドだけでなく、すべての受信のサブユニット コマンド、ピアのサブユニット ドライバー スタックが実装されている場合にルーティングされるメモ、[仮想サブユニット ドライバー スタック](virtual-subunit-driver-stack.md)します。

### <a name="unit-command-extension-mechanism"></a>**単位コマンド拡張機能のメカニズム**

ピアのサブユニット ドライバー スタックのコンテキストでは、ターゲットの機能は、AV/C 単体のコマンドのサポートに制限されます。 (仮想のサブユニットまたはピアのサブユニット) 用のサブユニット ドライバーを登録し、AV/C 要求を受信する場合*Avc.sys*サブユニットのみをサポートしている\_情報 (0x31) と単位\_情報 (0x30) オペコードで直接します。 オペコードの詳細については、次を参照してください。、 *AV/C デジタル インターフェイス コマンド Set 全般の仕様、Rev 3.0*します。 CCM プロトコルまたは DTCP などの追加の単体のコマンドをサポートするために*Avc.sys*プラグイン拡張メカニズムを提供します。 サブユニットまたは WDM フィルター ドライバーの任意の数がでサポートされるユニットのオペコードを登録、 **AlternateOpcodes**のメンバー、 [ **AVC\_コマンド\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avc_command_irb)を通じて送信された構造体、 [ **AVC\_関数\_取得\_要求**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-get-request)関数。 **AlternateOpcodes**はカウント対象のバイト配列は要素 0 は、代替のオペコードで残りのバイト数。 **AlternateOpcodes**代替オペコードは、単位の要求を処理するときに非表示にする必要はありませんので、応答を送信するときは無視されます。

組み込みの拡張メカニズムを使用するには、0 xff でとして単位アドレスを指定、 **SubunitAddress** 、AVC のメンバー\_コマンド\_IRB 構造体。 **SubunitAddress**メンバーのでは、単独で左単体のコマンド (のサブユニットでドライバーがまだ存在していればそのアドレス単位)。 仮想のサブユニット ドライバーにすることは常にオフのキー、 **SubunitAddress**メンバー。

 

 




