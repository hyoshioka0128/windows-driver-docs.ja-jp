---
title: Hklm \system\currentcontrolset\services レジストリ ツリー
description: Hklm \system\currentcontrolset\services レジストリ ツリーでは、システム上のサービスに関する情報を格納します。
ms.assetid: c966b029-8171-4db7-9fbb-3a4222ff184b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a705e118b4863cf39610a5baf8415fbf0b161c1d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553409"
---
# <a name="hklmsystemcurrentcontrolsetservices-registry-tree"></a>HKLM\\システム\\CurrentControlSet\\サービスのレジストリ ツリー





**HKLM\\システム\\CurrentControlSet\\サービス**レジストリ ツリーは、システムの各サービスに関する情報を保存します。 各ドライバーは、フォームのキーを持つ**HKLM\\システム\\CurrentControlSet\\サービス\\**<em>DriverName</em>します。 PnP マネージャー内のドライバーのこのパスを渡す、 *RegistryPath*ドライバーの呼び出し時にパラメーター [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチン。 ドライバーがドライバーの定義済みのグローバルなデータでそのキーの下を格納できる、**サービス**ツリー。 このキーの下に格納されている情報は初期化中にドライバーを使用できます。

次のキーと値のエントリは、特に興味深いは。

<a href="" id="imagepath"></a>**ImagePath**  
ドライバーのイメージ ファイルの完全修飾パスを指定する値のエントリ。 Windows では、必要なを使用してこの値を作成します。 **ServiceBinary**ドライバーの INF ファイルのエントリ。 このエントリは存在、*サービス-インストール セクション*ドライバーのによって参照される[ **INF AddService ディレクティブ**](inf-addservice-directive.md)します。 このパスの一般的な値は *%systemroot%*\\*system32\\ドライバー\\DriverName*、.sys、 *DriverName*はドライバーの名前**サービス**キー。

<a href="" id="parameters"></a>**パラメーター**  
ドライバー固有のデータを格納するために使用するキー。 ドライバーの一部の種類では、システムで特定の値のエントリを検索する必要があります。 このサブキーを使用する値のエントリを追加する**AddReg**ドライバーの INF ファイル内のエントリ。

<a href="" id="performance"></a>**パフォーマンス**  
省略可能なパフォーマンスを監視するための情報を指定するキー。 このキーの値は、その DLL 内のドライバーのパフォーマンス DLL の名前と特定のエクスポートされた関数の名前を指定します。 このサブキーを使用する値のエントリを追加する**AddReg**ドライバーの INF ファイル内のエントリ。

 

 





