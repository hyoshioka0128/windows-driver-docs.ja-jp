---
title: ピア サブユニット ドライバー スタック
description: ピアサブユニットドライバースタック
ms.assetid: 6ef4b6ae-3802-4ba9-acfa-4b3edba11ba3
keywords:
- ピアサブユニットドライバースタック WDK AV/C
- ドライバースタック WDK AV/C
- スタック WDK AV/C
- サブユニットは WDK AV/C をサポートします
- AV/C WDK、ドライバースタック
- 単体コマンド WDK AV/C
- 組み込みの拡張メカニズム WDK AV/C
- コマンド拡張機能のメカニズム WDK AV/C
- コマンドターゲット WDK AV/C
- Avc.sys 関数ドライバー WDK、ドライバースタック
ms.date: 06/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: 0b731501748187119ebc47953878f9584ff4a559
ms.sourcegitcommit: 31fa7dbbcd051d7ec1ea3e05a4c0340af9d3b8a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85073424"
---
# <a name="peer-subunit-driver-stack"></a>ピアサブユニットドライバースタック

ピアドライバースタックは、IEEE 1394 バス上でアクティブであり、コンピューターから制御できる AV/C サブユニットを表すために読み込まれたドライバーで構成されます。 外部デバイスコントロールは、AV/C ピアドライバースタックを介して開始する必要があります。 Windows は、デバイスがシステムに接続されている (またはシステムの起動時に存在する) たびに、IEEE 1394 バス上の外部 AV/C デバイスごとに*Avc.sys*のインスタンスを読み込みます。 ピアサブユニットドライバーをサポートするために読み込まれる*Avc.sys*の各インスタンスは、GUID AVC クラスのデバイスインターフェイスの新しいインスタンスを登録 \_ \_ します。 GUID avc クラスのデバイスインターフェイスの詳細については \_ \_ 、「Avc.sysと[**IOCTL \_ AVC \_ クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_class)の[使用](using-avc-sys.md)」を参照してください。

ピアサブユニットドライバー \_ \_ は、 *Avc.sys*によってエクスポートされる IOCTL AVC クラスインターフェイスを介して、サブユニットにアクセスして制御します。 *Avc.sys*は、AV/C コマンドと応答プロトコルを処理します。これには、IEC 61883 関数制御プロトコル (FCP) とのすべてのやり取りが含まれます。 ただし、ピアサブユニットドライバーは、必要に応じて、特定の*61883.sys*機能と通信したり、直接アクセスしたりすることはできません。 サブユニットドライバーが、Microsoft がサポートしていないストリーム形式を使用する AV/C サブユニットを表している場合は、 *61883.sys*と直接通信する必要がある場合があります。 サブユニットドライバーは、必要に応じて、 **IOCTL \_ 61883 \_ クラス**インターフェイスを使用して、 *61883.sys*と直接通信できます。 Microsoft では、DV および MPEG2 形式のストリーミングをサポートする低フィルタードライバーである*Avcstrm.sys*を提供しています。 *Avcstrm.sys*の詳細については、「 [AV/C ストリーミングの概要](av-c-streaming-overview.md)」を参照してください。

ピアサブユニットドライバーは、外部の AV/C デバイスからの通知を受け取り、AV/C コマンドを受信するように登録できます。 登録するために、ピアサブユニットドライバーは、IOCTL AVC クラスの i/o 制御コードの**Iocontrolcode**メンバーと、avc 関数 GET 要求に設定された subfunction を使用して、 [**irp \_ MJ \_ 内部 \_ デバイス \_ 制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)i/o 要求パケット (irp) を発行し \_ \_ \_ \_ \_ ます。 この機能により、ピアサブユニットドライバーはサブユニットから AV/C 要求を受信し、接続と互換性の管理 (CCM) プロトコルやデジタル伝送 Content Protection (DTCP) などの仕様のサポートを有効にすることができます。 CCM の詳細については、「 [IEEE 1394 取引の関連付け](https://1394ta.org/library-2/)」 web サイトを参照してください。 DTCP の詳細については、[デジタル伝送ライセンス管理者](https://www.dtcp.com/)web サイトを参照してください。

この機能は、仮想 AV/c サブシステムドライバーをサポートして、コンピューターに AV/C コマンドを送信する (サブシステムドライバーが仮想 AV/C デバイススタックに配置されている) ことを前提としています。また、外部デバイスの AV/C サブユニットがコンピューターシステムに AV/C コマンドを送信することを許可しません。

## <a name="peer-stack-as-avc-command-target"></a>AV/C コマンドターゲットとしてのピアスタック

ピアサブユニットドライバースタックには、ベンダー固有またはデバイス固有のターゲット AV/C 機能を提供する追加の WDM フィルタードライバーを含めることができます。 このピアサブユニットドライバースタック拡張メカニズムを使用すると、サードパーティベンダーは、5C コピー防止などの付加価値機能、および Microsoft が提供する AV/C 実装の拡張機能を個別に実装できます。

サブユニットドライバーはこの機能を実行できますが、複数のサブユニットを持つデバイスの場合は、WDM フィルタードライバーを使用することをお勧めします。 上位ドライバー (サブユニットまたはフィルタードライバー) が[**AVC \_ 関数の \_ GET \_ 要求**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-get-request)によって受信要求を受信するように登録されている場合、コンピューターは AV/C ターゲットとしてのみ公開されます。 AV/C ユニットコマンドの詳細については、「 [**AVC \_ 関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)」を参照してください。

ドライバーの読み込みは、デバイス識別子 (Id) に基づいています。そのため、ユニットの機能は、デバイス固有またはベンダー固有の単位で選択的に読み込むことができます。 仮想サブユニットドライバースタックでは、このメカニズムが一般的にサポートされています (デバイス固有の方法ではありません)。

ピアサブモジュールドライバースタックがデバイス固有のユニット拡張を実装している場合は、すべての未処理のユニットコマンドと、すべての受信サブユニットコマンドが仮想サブモジュール[ドライバースタック](virtual-subunit-driver-stack.md)にルーティングされることに注意してください。

## <a name="unit-command-extension-mechanism"></a>Unit コマンド拡張機能のメカニズム

ピアサブユニットドライバースタックのコンテキストでは、ターゲット機能は AV/C ユニットコマンドのサポートに限定されます。 サブユニットドライバー (仮想サブユニットまたはピアサブユニット用) が AV/C 要求を受信するように登録されている場合、 *Avc.sys*は、サブユニット \_ 情報 (0X31) と UNIT \_ info (0x30) のオペコードのみを直接サポートします。 オペコードの詳細については、「 *AV/C Digital Interface Command Set General Specification, Rev 3.0*」を参照してください。 CCM プロトコルや DTCP などの追加の単位コマンドをサポートするために、 *Avc.sys*にはプラグイン拡張メカニズムが用意されています。 任意の数のサブユニットまたは WDM フィルタードライバーは、 [**avc \_ 関数 \_ GET \_ REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-get-request)関数を介して送信された[**Avc \_ コマンド \_ IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_command_irb)構造体の**alternateopcodes**メンバーを介して、サポートする単体オペコードを登録できます。 **Alternateopcodes**は、カウントされたバイト配列です。要素0は、残りのバイトの代替オペコードの数です。 応答の送信時に**Alternateopcodes**は無視されるため、単体要求を処理するときに代替オペコードを非表示にする必要はありません。

組み込みの拡張メカニズムを使用するには、AVC コマンド IRB 構造体の**Subunitaddress**メンバーで、単位のアドレスを0xff として指定し \_ \_ ます。 **Subunitaddress**メンバーは、単位コマンドに対してだけで残されています (サブユニットドライバーによって提供されるユニットアドレスはまだ存在しています)。 仮想サブユニットドライバーは、常に**Subunitaddress**メンバーからキーを切ることができます。
