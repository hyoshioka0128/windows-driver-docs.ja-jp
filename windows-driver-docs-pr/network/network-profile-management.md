---
title: ネットワーク プロファイルの管理
description: ネットワーク プロファイルの管理
ms.assetid: 8f430502-e436-40c2-a993-c4f1e737076a
keywords:
- IHV 拡張 DLL WDK ネイティブ 802.11、ネットワーク プロファイル
- ネットワーク プロファイル WDK ネイティブ 802.11 IHV 拡張 DLL
- 802.11 IHV 拡張 DLL の WDK のネイティブ ネットワーク プロファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecb175950ca3b8dcd10df8f673b3884f8e9a40ce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361836"
---
# <a name="network-profile-management"></a>ネットワーク プロファイルの管理




 

このセクションでは、管理とネットワークの IHV 拡張 DLL でのプロファイルの処理について説明します。 ネットワーク プロファイルは、基本的なサービス (BSS) ネットワークに接続操作の属性を定義します。

IHV 拡張機能の DLL は、検証や、ネットワーク プロファイルに専用の拡張機能を作成します。 これらの拡張機能は、各フラグメント内で宣言して、XML データ フラグメントを**IHV**ネイティブ 802.11 XML スキーマの要素。 内のデータ、 &lt;IHV&gt;と&lt;/IHV&gt;のタグ、 **IHV**要素は IHV によって定義された形式。 ネイティブの 802.11 XML スキーマの詳細については、Microsoft Windows SDK のマニュアルを参照してください。

ここでは、次のトピックについて説明します。

[ネットワーク プロファイルの概要](network-profile-overview.md)

[ネットワーク プロファイルの拡張機能の作成](creating-network-profile-extensions.md)

[ネットワーク プロファイルの拡張機能を検証しています](validating-network-profile-extensions.md)

 

 





