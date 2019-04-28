---
title: ファイル マップのネットワーク ドライブ
description: ファイル マップのネットワーク ドライブ
ms.assetid: 55a5523f-5735-4b44-8d98-ded9932e630a
keywords:
- ファイル マップのネットワーク ドライブ
- シェル コマンドでは、ファイルのマップのネットワーク ドライブ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9fc898edc99e4fee25e9f37e0b80f46d0e819a36
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380238"
---
# <a name="file--map-network-drive"></a>File | Map Network Drive (ファイル | ネットワーク ドライブの割り当て)


## <span id="ddk_file_map_network_drive_dbg"></span><span id="DDK_FILE_MAP_NETWORK_DRIVE_DBG"></span>


をクリックして**ネットワーク ドライブの割り当て**上、**ファイル**] メニューの [ネットワーク接続を追加し、これらの接続にドライブ文字を割り当てます。

### <a name="span-iddialogboxspanspan-iddialogboxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>ダイアログ ボックス

クリックすると**ネットワーク ドライブの割り当て**、**ネットワーク ドライブの割り当て** ダイアログ ボックスが表示されます。 使用して、**ドライブ**と**フォルダー**メニューをサーバーと共有を選択し、ドライブ文字を割り当てます。

このダイアログ ボックスは、Windows エクスプ ローラーの対応する機能とまったく同じように動作します。

**ファイル |ネットワーク ドライブのマップ**コマンド WinDbg を実行しているコンピューターのネットワーク接続のみに影響を与えます。 リモート デバッグ セッションでクライアントとして WinDbg を使用して、サーバーのネットワーク接続を変更して、使用する必要があります、 **.shell して net use**コマンド。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

コマンド シェルにアクセスする方法の詳細については、次を参照してください。[シェル コマンドを使用して](using-shell-commands.md)します。

 

 





