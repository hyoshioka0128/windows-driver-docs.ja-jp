---
title: UMDF オブジェクトの表示
description: このトピックでは、Wudfext.dll デバッガー拡張機能を使用して、ユーザー モード ドライバー フレームワーク (UMDF) バージョン 1 のドライバーによって使用されるオブジェクトに関する情報を表示する方法について説明します。
ms.assetid: 36d0d604-3ed1-4ca7-b5bd-207942ecfc1e
keywords:
- デバッグ シナリオ WDK UMDF、UMDF オブジェクトの表示
- UMDF WDK、デバッグ シナリオ、UMDF オブジェクトの表示
- UMDF WDK、UMDF オブジェクトの表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08f723e30d418385b7f51bb8fdf3c619ce3507d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372158"
---
# <a name="viewing-umdf-objects"></a>UMDF オブジェクトの表示

[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

このトピックでは、Wudfext.dll デバッガー拡張機能を使用して、ユーザー モード ドライバー フレームワーク (UMDF) バージョン 1 のドライバーによって使用されるオブジェクトに関する情報を表示する方法について説明します。

以降 UMDF バージョン 2 では、代わりに、Wdfkd.dll デバッガー拡張機能を使用する必要があります。 詳細については、次を参照してください。 [Windows ドライバー フレームワークの拡張機能 (Wdfkd.dll)](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-)します。

UMDF バージョン 1 のオブジェクトに関する情報を表示するのには、次の手順を実行できます。

1.  ホスト プロセス内にあるデバイスの履歴を表示するのにには、次の UMDF デバッガー拡張機能の 1 つを使用します。
    -   **! wudfext.umdevstacks**
    -   **! wudfext.umdevstack**次の例に示すようにします。

        **! wudfext.umdevstack &lt;dev-スタック-addr&gt;**

        情報には、ドライバーのオブジェクトと各ドライバーのデバイス オブジェクトが含まれています。 現時点では、UMDF できデバイス スタックの 1 つだけホスト プロセスでこれら 2 つの拡張機能の出力の違いはありません。

2.  使用して、完全なオブジェクトのツリーを表示、 **! wudfext.wudfobject** UMDF デバッガー拡張機能の次の例のように。

    **!wudfext.wudfobject &lt;IWDFDriver\*&gt; 1**

3.  使用して、 **! wudfext.wudfdevice** UMDF デバッガー拡張が、プラグ アンド プレイ (PnP) を決定する次の例と、デバイスの電源管理の状態で示すようにします。

    **! wudfext.wudfdevice &lt;IWDFDevice\*&gt;**

4.  デバイスに関連付けられているキューを確認するには、次の手順に従います。
    1.  使用して、 **! wudfext.wudfdevicequeues** UMDF デバッガー拡張がデバイスに関連付けられているキューを表示します。 この拡張機能は、キューのプロパティ、キューの状態、およびドライバーが所有している要求を示します。
    2.  使用して、 **! wudfext.wudfqueue** UMDF デバッガー拡張が各キューに関する情報を取得する次の例に示すようにします。

        **! wudfext.wudfqueue &lt;IWDFIoQueue\*&gt;**

5.  使用して、 **! wudfext.wudfrequest** UMDF デバッガー拡張が特定の要求に関する情報を取得します。 この情報には、基になるユーザー モード I/O 要求パケット (IRP) が含まれています。 ユーザー モードの IRP 情報から、スタックで、要求が現在処理される場所を決定できます。 使用することも、 **! wudfext.umirp** UMDF デバッガー拡張がこのユーザー モード IRP の情報を取得します。

6.  によってすべての I/O ターゲットを決定します。

    1.  使用して、 **! wudfext.wudfobject** UMDF デバッガーの拡張機能のデバイス オブジェクトの子オブジェクトを表示します。 I/O ターゲット オブジェクトは、デバイス オブジェクトの子オブジェクトです。
    2.  使用して、 **! wudfext.wudfiotarget** UMDF デバッガー拡張が各 I/O ターゲット オブジェクトに関する情報を表示する次の例で示すようにします。

        **!wudfext.wudfiotarget &lt;IWDFTarget\*&gt;**

        この拡張機能には、ターゲットの状態と送信した要求の一覧が表示されます。

    現在、すべての I/O ターゲットを表示することができます UMDF デバッガーの拡張機能はありません。

7.  次の UMDF デバッガー拡張機能を使用すると、ファイル オブジェクトに関する情報を表示します。

    <a href="" id="-wudfext-wudfrequest-or--wudfext-umirp"></a> **! wudfext.wudfrequest**または **! wudfext.umirp**  
    使用して、 **! wudfext.wudfrequest**または **! wudfext.umirp** UMDF デバッガー拡張がデバイス オブジェクトの子オブジェクトであるファイルの表示にします。

    <a href="" id="-wudfext-wudffile"></a> **!wudfext.wudffile**  
    使用して、 **! wudfext.wudffile** UMDF デバッガー拡張が framework ファイルに関する情報を表示する次の例で示すようにします。

    **! wudfext.wudffile &lt;IWDFFile\*&gt;**

    <a href="" id="-wudfext-umfile"></a> **! wudfext.umfile**  
    使用して、 **! wudfext.umfile** UMDF 内スタック ファイル (つまり、ファイル オブジェクトによって作成されたファイル オブジェクトではなく、スタック内のドライバーの作成に関する情報を表示する次の例で示すように、UMDF デバッガー拡張機能アプリケーションまたは別のスタック内のドライバーによって)。

    **! wudfext.umfile &lt;addr&gt;**

    場合によっては、対応するフレームワーク ファイルを表示できない可能性があり、ユーザー モード IRP の情報には、UMDF のスタック内のファイルが含まれます。

    情報を **! wudfext.umfile**表示には UMDF のスタック内のファイルをキューに置かれたすべての Irp が含まれています。 のみドライバーで作成されたファイルは、それらのファイルをキューに置かれたユーザー モード Irp を追跡します。 ファイルのアプリケーションで作成された場合は、I/O マネージャーは、カーネル モード Irp を追跡します。

    <a href="" id="-wudfext-umdevstacks-and--wudfext-umdevstack"></a> **! wudfext.umdevstacks**と **! wudfext.umdevstack**  
    出力を使用して、 **! wudfext.umdevstacks**と **! wudfext.umdevstack** UMDF ドライバーで作成されたファイルに対応する未処理の UMDF 内スタック ファイルを表示のデバッガー拡張機能。

 

 





