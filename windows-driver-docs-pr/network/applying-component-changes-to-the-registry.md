---
title: レジストリへのコンポーネントの変更の適用
description: レジストリへのコンポーネントの変更の適用
ms.assetid: f844a693-cf26-407c-b182-b652a4c585b4
keywords:
- オブジェクトの WDK ネットワーク、レジストリ値への通知します。
- ネットワーク オブジェクト、WDK のレジストリ値を通知します。
- レジストリ WDK オブジェクトに通知します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f170a0910b0067dd47b957d93e1b993d4d07458e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367709"
---
# <a name="applying-component-changes-to-the-registry"></a>レジストリへのコンポーネントの変更の適用





後は、ネットワーク構成のサブシステムが通知オブジェクトを呼び出します[ **INetCfgComponentControl::ApplyRegistryChanges** ](https://msdn.microsoft.com/library/windows/hardware/ff547727)メソッド、通知オブジェクトが設定、変更、またはからの情報を削除します通知オブジェクトによって以前に実行されるアクションに応じてレジストリ。 通知オブジェクトがインストール、削除、またはオブジェクトを所有するコンポーネントのパラメーターの変更に関連する特定のアクションを実行した後、通知オブジェクトは、実行されるアクションを示すデータ メンバーを設定する必要があります。 サブシステムの呼び出し後**ApplyRegistryChanges**をレジストリに構成の変更を適用する**ApplyRegistryChanges**レジストリを変更する方法については、このデータ メンバーを使用する必要があります。 次に、例を示します。

-   通知オブジェクトが以前に関連するオブジェクトを所有するコンポーネントをインストールする操作を実行している場合、通知オブジェクトが「インストール」アクションを示すデータ メンバーを設定が必要があります。 サブシステムの呼び出し後**ApplyRegistryChanges**をレジストリに構成の変更を適用する**ApplyRegistryChanges**コンポーネントに関する情報がレジストリに設定する必要があります。

-   通知オブジェクトが以前に関連オブジェクトを所有するコンポーネントを削除する操作を実行している場合、通知オブジェクトが「削除」操作を示すデータ メンバーを設定が必要があります。 サブシステムの呼び出し後**ApplyRegistryChanges**をレジストリに構成の変更を適用する**ApplyRegistryChanges**コンポーネントに関する情報をレジストリから削除する必要があります。

-   コンポーネントのカスタム プロパティのいずれかのページし、コンポーネントのパラメーターまで、コンポーネントのいずれかの変更は、ユーザー表示通知オブジェクトにデータ メンバーを設定する必要がありますがある場合は、「パラメーターの変更」としてアクションを示すです。 サブシステムの呼び出し後**ApplyRegistryChanges**をレジストリに構成の変更を適用する**ApplyRegistryChanges**レジストリのコンポーネントのパラメーターに関する情報を変更する必要があります。

開き、コンポーネントに関する情報を変更するコンポーネントのレジストリ キーの取得、 **ApplyRegistryChanges**を呼び出して、コンポーネントのメソッドを実装する必要があります[ **INetCfgComponent::OpenParamKey** ](https://msdn.microsoft.com/library/windows/hardware/ff547890)メソッド。 コンポーネントのレジストリ キーの下のレジストリの値を設定するには、実装**ApplyRegistryChanges** Win32 関数を使用してデータをレジストリに書き込めません。 たとえば、 **ApplyRegistryChanges**呼び出すことができます、 **RegCreateKeyEx**関数の値を保持するために、サブキーを作成して、 **RegSetValueEx**関数を作成し、それらを設定値。

レジストリに関する詳細については、データを書き込むと、そこからデータを取得するには、Microsoft Windows SDK が参照してください。

 

 





