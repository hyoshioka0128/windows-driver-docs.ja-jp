---
title: SRV_OPEN 構造体
description: SRV_OPEN 構造体
ms.assetid: 6cf4c6f6-a21f-4919-92b5-2403b650d8d0
keywords:
- サーバーは、WDK RDBSS を開く
- WDK RDBSS のサーバーを開く
- SRV_OPEN 構造体
- データ構造体の WDK ファイル システム
- RDBSS WDK ファイル システム、接続およびファイル構造
- リダイレクトされたサブシステムの WDK のバッファリングをドライブのファイル システム、接続およびファイル構造
- 接続が WDK RDBSS 構造体します。
- ファイル構造 WDK RDBSS
- WDK RDBSS 構造体
- WDK RDBSS の接続情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19af10d64c1f5d4200dcef515f113d26c83a4654
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549256"
---
# <a name="the-srvopen-structure"></a>SRV\_オープン構造体


## <span id="ddk_the_srv_open_structure_if"></span><span id="DDK_THE_SRV_OPEN_STRUCTURE_IF"></span>


SRV\_オープン構造体は、サーバー上、開いているファイルをについて説明します。 複数のファイル オブジェクトとファイル オブジェクトの拡張機能 (FOBXs) を共有する同じ SRV\_アクセス権が一致する場合、開いている構造体。 たとえば、ファイル ID が格納 Smb 向けです。 ファイルの Id の一覧は、FCB に関連付けられます。 同様に、同じサーバー側のオープンを共有するすべてのファイル オブジェクト拡張子次にまとめて示します。 また、FCB の新しいオープンが、サーバー側の開いているコンテキストを共有するかどうかに関する情報が格納されます。

SRV に影響するフラグ値\_オープン操作は、2 つのグループに分割されます。

-   ネットワークのミニ リダイレクターに表示されるフラグ

-   RDBSS とネットワークのミニ リダイレクターを非表示を内部的に使用されるプライベート フラグ

ネットワークのミニ リダイレクターに表示されるフラグは、可能な SRV の下位 16 ビットで構成されている\_フラグ。 上位 16 ビットは、RDBSS によって内部的に使用するため予約されています。

SRV\_構造体開くにはには、次が含まれています。

-   署名と参照カウント

-   FCB 構造体への戻りポインター

-   V に戻りポインター\_NET\_ルート構造体 (通常は)

-   FOBX 構造の一覧

-   アクセス権と collapsibility 状態

-   ネットワークのミニ リダイレクターまたは SRV の作成者によって要求された追加のストレージ\_オープン構造体

 

 




