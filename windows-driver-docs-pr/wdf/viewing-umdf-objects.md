---
title: UMDF オブジェクトの表示
description: このトピックでは、Wudfext のデバッガー拡張機能を使用して、ユーザーモードドライバーフレームワーク (UMDF) バージョン1ドライバーによって使用されるオブジェクトに関する情報を表示する方法について説明します。
ms.assetid: 36d0d604-3ed1-4ca7-b5bd-207942ecfc1e
keywords:
- デバッグシナリオ WDK UMDF、UMDF オブジェクトの表示
- UMDF WDK, デバッグシナリオ, UMDF オブジェクトの表示
- UMDF WDK、UMDF オブジェクトの表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef76bb5911a3c447150025eef1158b594d1502e6
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210856"
---
# <a name="viewing-umdf-objects"></a>UMDF オブジェクトの表示

[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

このトピックでは、Wudfext のデバッガー拡張機能を使用して、ユーザーモードドライバーフレームワーク (UMDF) バージョン1ドライバーによって使用されるオブジェクトに関する情報を表示する方法について説明します。

UMDF バージョン2以降では、代わりに、Wdfkd デバッガー拡張機能を使用する必要があります。 詳細については、「 [Windows Driver Framework Extensions (Wdfkd .dll)](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-)」を参照してください。

次の手順を実行して、UMDF version 1 オブジェクトに関する情報を表示できます。

1.  次のいずれかの UMDF デバッガー拡張機能を使用して、ホストプロセス内のデバイススタックを表示します。
    -   **! wudfext. umdevstacks**
    -   次の例に示すように、" **! wudfext. umdevstack** " と表示されます。

        **! wudfext. umdevstack &lt;dev-stack-addr&gt;**

        この情報には、各ドライバーのドライバーオブジェクトとデバイスオブジェクトが含まれています。 現在、UMDF ではホストプロセス内のデバイススタックが1つしか許可されていないため、これら2つの拡張機能の出力に違いはありません。

2.  次の例に示すように、 **! wudfext. wudfext**の UMDF デバッガー拡張機能を使用して、完全なオブジェクトツリーを表示します。

    **! wudfext. wudfext &lt;IWDFDriver\*&gt; 1**

3.  次の例に示すように、 **! wudfext. wudfext**の UMDF デバッガー拡張機能を使用して、デバイスのプラグアンドプレイ (PnP) と電源管理の状態を確認します。

    **! wudfext &lt;IWDFDevice\*&gt;**

4.  デバイスに関連付けられているキューを特定するには、次の手順を実行します。
    1.  デバイスに関連付けられているキューを表示するには、 **! wudfext. wudfdevicequeues**の UMDF デバッガー拡張機能を使用します。 この拡張機能には、キューのプロパティ、キューの状態、およびドライバー所有の要求が表示されます。
    2.  各キューに関する情報を取得するには、次の例に示すように、 **! wudfext. wudfext**の UMDF デバッガー拡張機能を使用します。

        **! wudfext &lt;IWDFIoQueue\*&gt;**

5.  特定の要求に関する情報を取得するには、 **! wudfext. wudfext** UMDF デバッガー拡張機能を使用します。 この情報には、基になるユーザーモード i/o 要求パケット (IRP) が含まれます。 ユーザーモードの IRP 情報から、現在スタック内で要求が処理されている場所を確認できます。 また、 **! wudfext. umirp** UMDF デバッガー拡張機能を使用して、このユーザーモードの IRP 情報を取得することもできます。

6.  すべての i/o ターゲットを決定する方法:

    1.  **! Wudfext. wudfext**の UMDF デバッガー拡張機能を使用して、デバイスオブジェクトの子オブジェクトを表示します。 I/o ターゲットオブジェクトは、デバイスオブジェクトの子オブジェクトです。
    2.  次の例に示すように、 **! wudfext. wudfiotarget**の UMDF デバッガー拡張機能を使用して、各 i/o ターゲットオブジェクトに関する情報を表示します。

        **! wudfext. wudfext &lt;IWDFTarget\*&gt;**

        この拡張機能には、ターゲットの状態と送信された要求の一覧が表示されます。

    現在、すべての i/o ターゲットを表示できる UMDF デバッガー拡張機能はありません。

7.  次の UMDF デバッガー拡張機能を使用して、ファイルオブジェクトに関する情報を表示します。

    <a href="" id="-wudfext-wudfrequest-or--wudfext-umirp"></a>**! wudfext. wudfext**または **! wudfext. umirp**  
    デバイスオブジェクトの子オブジェクトであるファイルを表示するには、 **! wudfext. wudfext**または **! wudfext. umirp** UMDF デバッガー拡張機能を使用します。

    <a href="" id="-wudfext-wudffile"></a>**! wudfext. wudfext**  
    フレームワークファイルに関する情報を表示するには、次の例に示すように、 **! wudfext. wudfext**の UMDF デバッガー拡張機能を使用します。

    **! wudfext &lt;IWDFFile\*&gt;**

    <a href="" id="-wudfext-umfile"></a>**! wudfext umfile**  
    次の例に示すように、 **! wudfext ファイル**の umdf デバッガー拡張機能を使用して、umdf 内部スタックファイル (つまり、アプリケーションによって作成されたファイルオブジェクトや別のスタック内のドライバーによって作成されたファイルオブジェクトではなく、スタック内のドライバーが作成したファイルオブジェクト) の情報を表示します。

    **! wudfext. umfile &lt;addr&gt;**

    場合によっては、対応するフレームワークファイルが存在しないことがあります。また、ユーザーモードの IRP 情報には、UMDF in stack ファイルが含まれていることもあります。

    **! Wudfext umfile**には、UMDF 内部スタックファイルのキューに格納されている irp がすべて含まれます。 ドライバーで作成されたファイルのみが、これらのファイルのキューに登録されているユーザーモードの Irp を追跡します。 アプリケーションで作成されたファイルの場合、i/o マネージャーはカーネルモードの Irp を追跡します。

    <a href="" id="-wudfext-umdevstacks-and--wudfext-umdevstack"></a>**! wudfext. umdevstacks**と **! wudfext. umdevstacks**  
    **! Wudfext. umdevstacks**と **! wudfext**の umdf デバッガー拡張機能からの出力を使用して、ドライバーによって作成されたファイルに対応する未解決の umdf 内部スタックファイルを表示します。

 

 





