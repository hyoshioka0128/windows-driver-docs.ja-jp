---
title: タグの書き込み
description: タグの書き込み
ms.assetid: 916150D9-9A98-4463-81BE-7F46DF2694F4
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a82a2dc429beba49e724a62f452cf53d31a3103
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827344"
---
# <a name="tag-writing"></a>タグの書き込み


タグの書き込みは、カテゴリ (全般、NFC、およびすべて) に対して指定されます。 各カテゴリ内では、ドライバーは特定の種類のタグのみを認識します。

これらは、メッセージを任意の NearFieldProximity タグに書き込むことができる特別なパブリケーションです。 タグの既存のペイロードを上書きする必要があります。 追加セマンティクスは、NFC に対してのみ定義されます。 クライアントが上書きではなくを追加する場合は、元の NDEF メッセージを含む NDEF ペイロードを作成して "NDEF: WriteTag" パブリケーションに配置する必要があります。 任意の時点で、0個または1個の "\*: WriteTag" パブリケーションがアクティブになることが想定されています (ただし、適用されません)。

## <a name="general-tag-writing"></a>一般的なタグの書き込み


タグ書き込みは、NFC が有効になっていない NFP プロバイダーのオプション機能です。 ドライバーでは、パブリケーションに対してのみ次のタグの種類が認識される場合があります。

-   "WindowsUri: WriteTag"
-   "WindowsMime: WriteTag"
-   "Windows: WriteTag"

## <a name="nfc-tag-writing"></a>NFC タグの書き込み


NFC が有効になっている NFP プロバイダーには、タグ書き込みのサポートが必要です。 これらの要件を満たす必要があります。

近接通信テクノロジが NFC として提供されている場合、ドライバーは、パブリケーションに対してのみ次のタグの種類を認識する必要があります。

-   "WindowsUri: WriteTag"
-   "WindowsMime: WriteTag"
-   "Windows: WriteTag"
-   "NDEF: WriteTag"

厳密な NDEF エンコード規則は、NFC フォーラム仕様に従って使用されます。 たとえば、NDEF メッセージフラグメントは、有効な NDEF メッセージに続く場合でも書き込むことができません。

タグが NDEF 形式ではなく、メッセージが \*に対して公開されている場合は、NFC タグの  に**注意**してください。WriteTag では、プロバイダーはタグの書式を NDEF に設定し、ペイロードを書き込む必要があります。

 

## <a name="all-tag-writing"></a>すべてのタグの書き込み


タグの書き込みが NFP プロバイダーによってサポートされている場合、ドライバーはリストされているすべての要件を満たしている必要があります。

### <a name="required-actions"></a>必要なアクション

-   ドライバーは、"\*: WriteTag" サブスクリプションを認識できません。
-   1つ以上の "\*: WriteTag" パブリケーションが有効になっていて、十分な空き領域がある書き込み可能なタグがドライバーによって検出された場合、他のサブスクリプションと照合するために、タグの既存のペイロードを読み取ることはできません。 これにより、タグ書き込みアプリは、タグのメッセージにサブスクライブされている他のアプリやサービスをプリエンプトできます。
-   NFC が有効になっている NFP プロバイダーの場合、ドライバーは、nfc フォーラムタグとは対照的に、NFC フォーラムデバイスに接続しているときに "\*: WriteTag" パブリケーションを送信しないようにする必要があります。
-   少なくとも1つのペイロードに対して十分な空き領域がある書き込み可能なタグをドライバーが検出した時点で、1つ以上の "\*: WriteTag" パブリケーションが有効になっている場合、ドライバーは、そのタグにペイロードの1つだけを書き込む必要があります。 o 複数のパブリケーションがアクティブで、タグに書き込むのに十分な数のパブリケーションが存在する場合、最後に作成された、または有効になっている "\*: WriteTag" パブリケーションが書き込まれたものである必要があります。
-   ドライバーがペイロード用に十分な空き領域を持つ書き込み可能なタグと現在通信しているときに "\*: WriteTag" パブリケーションが作成または有効になっている場合、ドライバーは、以前にタグに書き込んだ場合でも、ドライバーはペイロードをタグに書き込む必要があります。
-   ドライバーは、前の内容が上書きされるようにタグに書き込む必要があります。
-   "\*: WriteTag" ペイロードがタグに正常に書き込まれた場合、ドライバーは、そのパブリケーションに対して指定されているように、次\_送信\_メッセージ処理 (前述のとおり) を使用して、 [**IOCTL\_NFP\_\_取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_get_next_transmitted_message)する必要があります。

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近距離無線近接 DDI リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

