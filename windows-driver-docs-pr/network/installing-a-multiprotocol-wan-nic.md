---
title: マルチ プロトコル WAN NIC のインストール
description: マルチ プロトコル WAN NIC のインストール
ms.assetid: 7000040c-8a26-496d-ae26-580aace68160
keywords:
- 追加レジストリ セクション WDK ネットワー キング、マルチ プロトコルの WAN NIC
- マルチ プロトコルの NIC WDK の WAN ネットワーク
- NIC WDK の WAN ネットワーク
- マルチ プロトコル WDK の WAN ネットワークの NIC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4054c796f9a0e268a98a7d735c442eb50139305
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324909"
---
# <a name="installing-a-multiprotocol-wan-nic"></a>マルチ プロトコル WAN NIC のインストール





マルチ プロトコルの WAN NIC は、1 つ以上の WAN プロトコルを提供します。 たとえば、このような NIC は ISDN、フレーム リレーを選択するユーザーを許可する場合があります。 または T1 チャネル化します。 ユーザーは、NIC を構成するときに、NIC またはインストール中に WAN のプロトコルを選択します。

> [!NOTE]
> ISDN 機能は、Windows 10 以降非推奨です。 


マルチ プロトコルの WAN NIC の仕入先には、ウィザードのページをインストールする共同インストーラーを提供する必要があります。 (共同インストーラーの詳細については、次を参照してください。[共同インストーラーの作成](https://msdn.microsoft.com/library/windows/hardware/ff554011))。 ウィザードのページには、WAN のプロトコルを選択するユーザーが表示されます。

-   ユーザーは、ISDN を選択する場合は、ISDN ウィザードが表示されます。 ISDN ウィザードでは、ISDN スイッチの種類と、選択したスイッチの種類、その他の ISDN パラメーターの値に応じてユーザーを入力します。 詳細については、次を参照してください。 [ISDN キーを指定すると、ISDN アダプターの値](specifying-isdn-keys-and-values-for-an-isdn-adapter.md)します。

-   ウィザードの追加のかどうか、ユーザーは、ISDN 以外 WAN のプロトコルを選択する、 **ShowIsdnPages**レジストリ値を WAN の NIC のインスタンスのキー。 この場合、ウィザードが設定**ShowIsdnPages** ISDN ウィザードを表示しないようにする 0 にします。 限り**ShowIsdnPages** 0 の場合は、ISDN ウィザードは表示されません。

WAN の NIC がインストールされた後、ユーザーは、NIC のプロパティ ページを使用して、NIC を再構成できます。

-   かどうか、ユーザーは、WAN の別のプロトコルに ISDN からプロトコルを変更、プロパティ ページを追加、 **ShowIsdnPages** WAN の NIC のインスタンスのキーが必要な場合にレジストリの値。 プロパティのページ セット**ShowIsdnPages**を 0 に ISDN ウィザードを表示しないようにします。

-   ユーザーには、ISDN、プロトコルが変更された場合、WAN の NIC のプロパティ ページには、変更を適用するユーザーに求めるダイアログ ボックスが表示されます。 プロパティ ページの設定、ユーザーは、変更を適用する場合**ShowIsdnPages**を 1 にします。 ユーザーは、NIC のプロパティ ページをもう一度が開いたら、ISDN ウィザードが表示されます。

なお、 **LowerRange**に ISDN をサポートするマルチ プロトコルの WAN NIC のバインド インターフェイスを設定する必要があります**isdn**します。 詳細については、次を参照してください。[バインド インターフェイスを指定する](specifying-binding-interfaces.md)します。 場合、 **ShowIsdnPages**レジストリ値が存在しない場合は、NIC の**LowerRange**に設定されている**isdn**のインストールと構成の中に、ISDN ウィザードが表示されますNIC 場合**ShowIsdnPages**設定は 0、ISDN ウィザードは表示されません。 場合**ShowIsdnPages**設定されている NIC の構成中に 1 に ISDN ウィザードが表示されます

 

 





