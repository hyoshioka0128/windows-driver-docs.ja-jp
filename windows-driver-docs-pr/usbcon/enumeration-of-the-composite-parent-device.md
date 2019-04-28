---
Description: 複合の USB デバイスの列挙体
title: 複合の USB デバイスの列挙体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b38f5fbe18724afd558c7af665eac0c8aee3af5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383018"
---
# <a name="enumeration-of-usb-composite-devices"></a>複合の USB デバイスの列挙体


新しい USB デバイスが接続するには、ホスト マシンを USB バス ドライバーはデバイスの物理デバイス オブジェクト (PDO) を作成し、PnP 新しい PDO を報告するイベントが生成されます。 オペレーティング システムは、ハードウェア Id に関連付けられた PDO のバス ドライバーを照会します。

すべての USB デバイス、USB バス ドライバー レポート、*デバイス ID*次の形式。

`USB\VID_xxxx&PID_yyyy`

**注**  *xxxx*と*yyyy*から直接取得された**idVendor**と**idProduct**デバイス記述子のフィールドそれぞれします。

 

バス ドライバーの互換性のある識別子 (ID) を報告も`USB\COMPOSITE`デバイスが、次の要件を満たしている場合。

-   デバイス記述子のデバイス クラスのフィールド (**bDeviceClass**) の値は 0、またはクラスを含める必要があります (**bDeviceClass**)、サブクラス (**bDeviceSubClass**)、およびプロトコル (**bDeviceProtocol**) デバイス記述子のフィールドがあります 0xEF や 0x01、0x02、値で説明したように、それぞれ[USB インターフェイスの関連付けの記述子](usb-interface-association-descriptor.md)します。

-   デバイスは、複数インターフェイスを実装する必要があります。

-   デバイスは、1 つの構成に必要です。

バス ドライバーでは、デバイスのクラスも確認します (**bDeviceClass**)、サブクラス (**bDeviceSubClass**)、およびプロトコル (**bDeviceProtocol**) のデバイスの記述子フィールド。 これらのフィールドは 0、デバイスが複合デバイス、およびバス ドライバー USB の互換性のある余分な識別子 (ID) を報告する場合\\PDO を合成します。

新しい PDO のハードウェアと互換性のある Id を取得した後は、オペレーティング システムは、INF ファイルを検索します。 INF ファイルの 1 つのデバイス ID と一致する場合は、Windows がその INF ファイルで示されているドライバーをロードおよび一般的な親ドライバーは作用しません。 INF ファイルには、デバイス ID、および PDO がない場合は、互換性 ID の検索を Windows 互換性のある ID を持つ Usb.inf で一致して、オペレーティング システムを起動すると、この、 [USB 汎用親ドライバー (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)します。

お使いのデバイスを管理する一般的な親ドライバーがデバイスには、システムが USB の互換性のある ID を生成することを確認するために必要な特性はありません\\複合では、ジェネリックをロードする INF ファイルを指定する必要が。親のドライバーです。 INF ファイルを含める必要があります、Usb.inf を参照するセクションには要件には/が含まれています。

複合デバイスに複数の構成がある場合は、どの構成を指定する必要がありますを指定する INF ファイルの一般的な親必要があります、レジストリで使用します。 必要なレジストリ キーについては、[既定以外の USB の構成を選択する構成で、Usbccgp.sys](selecting-the-configuration-for-a-multiple-interface--composite--usb-d.md)します。

## <a name="related-topics"></a>関連トピック
[一般的な親の USB ドライバー (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)  
[Microsoft 提供の USB ドライバー](system-supplied-usb-drivers.md)  



