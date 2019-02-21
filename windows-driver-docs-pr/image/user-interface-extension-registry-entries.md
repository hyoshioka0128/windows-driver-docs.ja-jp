---
title: ユーザー インターフェイスの拡張機能のレジストリ エントリ
description: ユーザー インターフェイスの拡張機能のレジストリ エントリ
ms.assetid: 1ddf12a1-50e9-4f6e-9394-5bb1afb67798
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc4c4acea8ef9c38149f4c2e93c51135ae29442b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537737"
---
# <a name="user-interface-extension-registry-entries"></a>ユーザー インターフェイスの拡張機能のレジストリ エントリ





COM サーバーのクラス ID は、各拡張機能を指定する必要があります。 各拡張機能の COM サーバーのクラス ID が CLSID レジストリ キー (値ではなく) として表示されていることに注意してください\\{WIA\_DIP\_UI\_CLSID}\\shellex、、WIA\_DIP\_。UI\_CLSID は、アプリケーションは、このプロパティを要求するときに返される実際の GUID。 レジストリ内のルックアップ キーの一部として、アプリケーションを使用します。 機能拡張インターフェイスごとできるさまざまなクラス ID を参照してください。 同じオブジェクトが実装し、それらの要件はありません。 実装されている拡張機能のみを一覧表示します。 4 つすべてを一覧表示する必要はありません。

クラス ID の GUID では、デバイスのすべてのモデルが同じドライバーを使用する場合を使用するには、どのドライバーが識別されるためそのすべてが同じクラス ID の GUID。 さまざまなモデルは、さまざまなドライバーを使用すると、異なる Guid が必要です。

<a href="" id="clsid--wia-dip-ui-clsid--shellex-contextmenuhandlers--clsid-of-com-in-process-server-"></a>CLSID\\{WIA\_DIP\_UI\_CLSID}\\shellex\\ContextMenuHandlers\\&lt;CLSID の COM インプロセス サーバー&gt;  
コンテキスト メニューの UI 拡張機能を実装する COM DLL をベンダーが提供されます。

<a href="" id="clsid--wia-dip-ui-clsid--shellex-propertysheethandlers--clsid-of-com-in-process-server-"></a>CLSID\\{WIA\_DIP\_UI\_CLSID}\\shellex\\PropertySheetHandlers\\&lt;CLSID の COM インプロセス サーバー&gt;  
プロパティ シートの UI 拡張機能を実装する COM DLL をベンダーが提供されます。

<a href="" id="clsid--wia-dip-ui-clsid--shellex-wiadialogextensionhandlers--clsid-of-com-in-process-server-"></a>CLSID\\{WIA\_DIP\_UI\_CLSID}\\shellex\\WiaDialogExtensionHandlers\\&lt;CLSID の COM インプロセス サーバー&gt;  
ベンダーがアプリケーション ダイアログの UI 拡張機能を実装する COM DLL を提供します。

<a href="" id="clsid--clsid-of-the-com-in-process-server--inprocserver32-default-value"></a>CLSID\\&lt;COM インプロセス サーバーの CLSID&gt;\\InProcServer32\\既定値  
REG\_SZ 型の機能拡張インターフェイスを実装する、ベンダーから提供された COM サーバーの名前を格納します。

<a href="" id="clsid--clsid-of-the-com-in-process-server--inprocserver32-threadingmodel"></a>CLSID\\&lt;COM インプロセス サーバーの CLSID&gt;\\InProcServer32\\ThreadingModel  
REG\_SZ 型のベンダーから提供された COM サーバーのスレッド処理モデルの名前を格納します。 このキーは、アパートメントに設定します。

 

 




