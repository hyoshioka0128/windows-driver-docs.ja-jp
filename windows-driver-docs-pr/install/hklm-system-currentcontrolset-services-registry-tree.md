---
title: HKLM\SYSTEM\CurrentControlSet\Services レジストリ ツリー
description: HKLM\SYSTEM\CurrentControlSet\Services レジストリツリーには、システム上の各サービスに関する情報が格納されます。
ms.assetid: c966b029-8171-4db7-9fbb-3a4222ff184b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 499163f56221235165958943c27549eecd9548d6
ms.sourcegitcommit: e480dcfea893ef6c85b2dfb5827f51b740466262
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2019
ms.locfileid: "71278369"
---
# <a name="hklmsystemcurrentcontrolsetservices-registry-tree"></a>HKLM\\SYSTEM\\CurrentControlSet\\Services レジストリツリー





**HKLM\\system\\CurrentControlSetServicesレジストリツリーには、システム上の各サービスに関する情報が格納されます。\\** 各ドライバーには、 **HKLM\\SYSTEM\\\\CurrentControlSet\\Services**の<em>ドライバー</em>の形式のキーがあります。 PnP マネージャーは、ドライバーの[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチンを呼び出すときに、ドライバーのこのパスを*RegistryPath*パラメーターに渡します。 ドライバーは、グローバルなドライバー定義データを、**サービス**ツリーのキーの**Parameters**サブキーの下に格納できます。 このキーの下に格納されている情報は、初期化中にドライバーで使用できます。

次のキーと値のエントリが特に重要です。

<a href="" id="imagepath"></a>**ImagePath**  
ドライバーのイメージファイルの完全修飾パスを指定する値のエントリ。 Windows は、ドライバーの INF ファイルの必須の**Servicebinary**エントリを使用して、この値を作成します。 このエントリは、ドライバーの[**INF AddService ディレクティブ**](inf-addservice-directive.md)によって参照される、 *service install セクション*にあります。 このパスの一般的な値は、 *% SystemRoot%* \\ *\\system32\\Drivers*のドライバー名です。この*名前は、* ドライバーの**サービス**キーの名前です。

<a href="" id="parameters"></a>**パラメータ**  
ドライバー固有のデータを格納するために使用されるキー。 ドライバーの種類によっては、特定の値のエントリを検索する必要がある場合があります。 このサブキーに値エントリを追加するには、ドライバーの INF ファイルの**AddReg**エントリを使用します。

<a href="" id="performance"></a>**速度**  
オプションのパフォーマンス監視に関する情報を指定するキー。 このキーの下の値は、ドライバーのパフォーマンス DLL の名前と、その DLL 内のエクスポートされた特定の関数の名前を指定します。 このサブキーに値エントリを追加するには、ドライバーの INF ファイルの**AddReg**エントリを使用します。

 

 





