---
title: 通知クラスの定義
description: 通知クラスの定義
ms.assetid: e21cf020-0bf8-4091-aac4-6324a680194a
keywords:
- オブジェクトの WDK ネットワークへの通知、クラスを通知
- ネットワーク WDK のオブジェクトへの通知、クラスを通知
- クラスの WDK ネットワークへの通知します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0ba6b7dfceafea70e5fb8ec62b7ec611db6407e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364248"
---
# <a name="defining-a-notify-class"></a>通知クラスの定義





通知から継承するように、クラスを実装する必要があります、 [ **INetCfgComponentControl** ](https://msdn.microsoft.com/library/windows/hardware/ff547725)インターフェイス。 ただし場合、次のインターフェイスから継承するように、通知のクラスを実装する必要がも特定の操作を実行するオブジェクトに通知します。

-   関連付けられている通知のクラスを継承する必要があります、通知オブジェクトは、インストール、アップグレード、およびオブジェクトを所有する、コンポーネントの削除に関連する操作を実行する場合、 [ **INetCfgComponentSetup** ](https://msdn.microsoft.com/library/windows/hardware/ff547758)インターフェイスです。

-   関連付けられている通知のクラスを継承する必要があります、通知オブジェクトには、オブジェクトを所有するコンポーネントのカスタム プロパティ ページが表示されている場合、 [ **INetCfgComponentPropertyUi** ](https://msdn.microsoft.com/library/windows/hardware/ff547738)インターフェイス。

-   関連付けられている通知のクラスを継承する必要があります通知オブジェクトは、ネットワーク構成のサブシステムが他のネットワーク コンポーネントにオブジェクトを所有するコンポーネントをバインドする方法の変更を評価する場合、 [INetCfgComponentNotifyBinding](https://msdn.microsoft.com/library/windows/hardware/ff547730)インターフェイス。

-   関連付けられている通知のクラスを継承する必要があります通知オブジェクトは、オブジェクトを所有するコンポーネントに影響を与えるネットワーク構成の変更を評価する場合、 [ **INetCfgComponentNotifyGlobal** ](https://msdn.microsoft.com/library/windows/hardware/ff547733)インターフェイスです。

クラスは、すべてに共通として定義する必要があります内のメンバーに通知する特定のデータ オブジェクトに通知します。 特定のデータ メンバーは、別のコンポーネントに定義する必要があります。 オブジェクトを定義する必要がありますすべて通知するデータ メンバーは次のとおりです。

-   型のオブジェクトを所有しているネットワーク コンポーネントのインスタンスへのポインター [ **INetCfgComponent** ](https://msdn.microsoft.com/library/windows/hardware/ff547715)インターフェイス。 通知オブジェクトのインスタンスでは、このポインターを使用して、アクセスし、オブジェクトを所有するコンポーネントを制御します。

-   型のネットワーク構成オブジェクトのインスタンスへのポインター [ **INetCfg** ](https://msdn.microsoft.com/library/windows/hardware/ff547694)インターフェイス。 通知オブジェクトのインスタンスでは、このポインターを使用して、ネットワーク構成のすべての側面にアクセスします。

-   通知オブジェクトを所有するコンポーネントのパラメーター情報を格納する変数

-   通知オブジェクトが以前に実行するアクションを指定する変数。 通知オブジェクトを実行する別の操作を示す定数を定義します。 ネットワーク構成のサブシステムが通知オブジェクトを呼び出すときに[ **INetCfgComponentControl::ApplyRegistryChanges** ](https://msdn.microsoft.com/library/windows/hardware/ff547727)メソッドに、レジストリ構成の変更を適用する**ApplyRegistryChanges**この変数を使用してレジストリを変更する方法を決定します。 たとえば、通知オブジェクトが以前に関連のオブジェクトを所有するコンポーネントをインストールする操作を実行する場合、 [ **INetCfgComponentSetup::Install** ](https://msdn.microsoft.com/library/windows/hardware/ff547762)メソッド、**インストール**インストールとしてアクションを示すには、この変数を設定する必要があります。

-   型のレジストリ キー **HKEY**します。 通知オブジェクトを呼び出す、 [ **INetCfgComponent::OpenParamKey** ](https://msdn.microsoft.com/library/windows/hardware/ff547890)を開き、コンポーネントのパラメーターを格納するレジストリ キーを取得するオブジェクトを所有するコンポーネントのメソッド。 通知オブジェクトを設定し、 **HKEY**キーへのメンバー。

コンス トラクターと、通知のクラスのデストラクターを定義します。 通知クラスのみを使用するプライベート メソッドを定義することも検討します。

すべての**IUnknown**通知クラスのインターフェイスのメソッドを実装する必要があります。 通知クラスは、上記の一覧に記載されている省略可能なインターフェイスのいずれかから継承している場合は、これらのインターフェイスのすべてのメソッドを実装しなければなりません。 注 E\_NOTIMPL は、通知オブジェクトのインターフェイスのメソッドのいずれかの有効な戻り値の型ではありません。 通知オブジェクトは、特定のメソッドの実装が必要としない場合、単純を返すメソッドを実装 S\_ok をクリックします。

 

 





