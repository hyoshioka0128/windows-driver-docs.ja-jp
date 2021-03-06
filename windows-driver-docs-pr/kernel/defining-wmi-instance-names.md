---
title: WMI インスタンス名の定義
description: WMI インスタンス名の定義
ms.assetid: 0f91710a-7bd2-462a-b677-6dd32160a861
keywords:
- WMI の WDK カーネルでは、イベント ブロック
- イベントは、WDK の WMI をブロックします。
- WDK の WMI のデータ ブロックします。
- WMI の WDK カーネルでは、データのブロック
- WDK の WMI をブロックします。
- WDK の WMI の名前の動的インスタンス
- 静的なインスタンス名を WDK WMI
- インスタンス名 WDK WMI
- WMI の WDK カーネルでは、インスタンス名
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33c0a37eae3a4be1bc428f14040cb44745cde398
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377100"
---
# <a name="defining-wmi-instance-names"></a>WMI インスタンス名の定義





*インスタンス*ブロックには WMI には、特定の物理デバイスまたはソフトウェア コンポーネントにより提供されるデータが含まれています。 ブロックの GUID は、ブロックを一意に識別すると同じようインスタンスの名前は、ブロックのインスタンスを一意に識別します。 WMI クライアント アプリケーションでは、インスタンス名を使用して、デバイスまたはデータを提供するコンポーネントとデータ ブロックで返される情報を関連付けます。 WMI では、インスタンス名を使用して、要求には、どのデバイスに送信するかを判断します。 インスタンス名を定義するときに、ドライバーは、PDO を使用して。 を強くお勧めします。

ドライバーは、2 つの方法のいずれかで、ブロックのインスタンス名を定義できます。

-   ドライバーの一覧を渡します*静的インスタンス名*WMI ブロックを登録するときにします。

    ブロックが登録されると、ドライバーと WMI インスタンス名を指定インデックスを使用してこの一覧にします。 静的なインスタンス名に基づいて、*デバイス インスタンス ID*のドライバーの PDO またはドライバーの定義の基本名。 または、ドライバー一覧を定義できますのインスタンス名の文字列。 ドライバー変更明示的にブロックを再登録することによってまで保持されます静的インスタンスの名前。

-   ドライバーが生成されます*動的インスタンス名*インスタンスを作成するとします。

    ドライバーでは、ブロックを登録する際にブロックの動的インスタンス名を生成することを示します。 ドライバーと WMI の両方が、バッファー内の文字列として動的にインスタンス名を渡す、ブロックが登録されると、 **Parameters.WMI.Buffer**します。

実行時にインスタンスの数またはインスタンス名、データ ブロックの変更頻度場合にのみ、ドライバーは動的なインスタンス名を生成する必要があります。 たとえば、ドライバー可能性がありますを使用して、プロセス Id または TCP/IP 接続の IP アドレス インスタンス名として。 このようなインスタンス名は、動的; である必要があります。静的な場合は、ドライバーはオーバーヘッドが増加するかなりを呼び出す必要がありますので[ **IoWMIRegistrationControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)変更が発生するたびに、数とインスタンスの名前を更新します。

ほとんどの場合は、静的インスタンス名はことをお勧めする理由は次の動的インスタンス名です。

-   静的なインスタンス名は、動的なインスタンス名にする必要がありますにドライバーが WMI の要求に対する応答でインスタンス名の文字列を返す必要がないために、ドライバーのパフォーマンスを向上します。

-   WMI は、登録時に静的なインスタンス名の競合を検出し、ドライバーの数、ブロックの登録に関係なく、特定のブロックのすべてのインスタンス名が一意ように、必要に応じて、インスタンス名を自動的に変更できます。

    WMI は、ドライバーを使用して一意の名前を生成するための動的インスタンス名、インスタンス名の競合を検出できない[ **IoWMIAllocateInstanceIds**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiallocateinstanceids)します。

-   ドライバーは、名前は、ドライバーの PDO またはドライバーの定義の基本名に基づいている限り、静的なインスタンスの名前を使用するブロックの Irp を処理するために、WMI のライブラリのルーチンを使用できます。

    ドライバーは、動的なインスタンスの名前を使用するデータ ブロックの Irp を処理するために WMI ライブラリ ルーチンを使用できません。

ドライバーは、ブロックが静的または動的なインスタンス名を使用し、静的インスタンスの型、名前、設定や WMIREG をクリアするかどうかを示します\_フラグ\_*XXX*で、 [ **WMIREGGUID** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-wmiregguidw)または[ **WMIGUIDREGINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/ns-wmilib-_wmiguidreginfo)構成ブロックを登録するときを WMI に渡されます。 詳細については、次を参照してください。 [WMI データ プロバイダーとして登録する](registering-as-a-wmi-data-provider.md)します。

 

 




