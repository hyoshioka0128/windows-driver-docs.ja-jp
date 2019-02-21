---
title: WMI の NDIS オブジェクト バージョンの問題
description: WMI の NDIS オブジェクト バージョンの問題
ms.assetid: 09440de8-125b-4155-9f28-c9f6893071b2
keywords:
- NDIS バージョンについて WDK には、WMI をサポートします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d80847483368d2f86f2b76e88b5b92ac8a42f744
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557708"
---
# <a name="ndis-object-version-issues-for-wmi"></a>WMI の NDIS オブジェクト バージョンの問題





このトピックでは、Windows Management Instrumentation (WMI) のサポートに影響を与える NDIS オブジェクト バージョンの問題について説明します。

WMI 管理オブジェクト フォーマット (MOF) ファイル内でバージョン管理はありません。 そのため、対応する NDIS 構造に新しいリビジョンがある場合は、MOF データ オブジェクトをより多くのフィールドが追加されています。

NDIS\_WMI\_Xxx\_ヘッダー構造体は、新しい NDIS バージョン以上のメンバーが追加されたときに新しいリビジョンをあります。 現在の NDIS の一覧については\_WMI\_Xxx\_ヘッダー構造体を参照してください[NDIS WMI 構造](https://msdn.microsoft.com/library/windows/hardware/ff567905)します。

クエリ操作の WMI 情報をアプリケーションにアクセスするときに、任意のデータにアクセスする前に返されたバッファーでバージョンを確認する必要があります。 設定操作では、アプリケーションを確認する必要があります、 **SupportedRevision** NDIS でメンバー\_WMI\_出力\_情報構造体の基になるドライバーが受け入れたバージョンを決定します。

多くの WMI オブジェクトを含む、 **MSNdis\_ObjectHeader**と等価であるプロパティ、 [ **NDIS\_オブジェクト\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff566588)構造体。 設定するときに、 **MSNdis\_ObjectHeader**プロパティ、設定、**型**と**リビジョン**に記載されているフィールド、 **NDIS\_オブジェクト\_ヘッダー**トピック。 64 ビット システムへのシームレスな移植性を確実には、設定、**サイズ**フィールドを`0xFFFF`します。

## <a name="related-topics"></a>関連トピック


[NDIS のバージョンの概要](overview-of-ndis-versions.md)

[NDIS バージョン情報を指定します。](specifying-ndis-version-information.md)

 

 






