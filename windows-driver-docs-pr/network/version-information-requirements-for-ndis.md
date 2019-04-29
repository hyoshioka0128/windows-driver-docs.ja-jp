---
title: NDIS のバージョン情報要件
description: NDIS のバージョン情報要件
ms.assetid: b2850077-271f-4bb6-8710-ae9415ad5eda
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18ed9eff0905c027d684da02ecd5c5da23d7f878
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387330"
---
# <a name="version-information-requirements-for-ndis"></a>NDIS のバージョン情報要件





NDIS は、NDIS バージョン間で一貫性のある動作が保証される各種のヘッダー バージョン情報要件をサポートします。 ヘッダーのバージョン情報をサポートするには、NDIS は次の責任があります。

-   下の改訂版を含む構造体を処理します。 つまり、NDIS はヘッダー情報をチェックし、ヘッダーのリビジョン情報に基づいて構造を解釈します。

-   関数呼び出しは失敗し、ドライバーは、正しくない構造体のリビジョンを使用している場合は、適切なエラー コードを返します。 NDIS は、NDIS 6.30 ドライバー Xxx を使用している場合、関数呼び出しに失敗など\_リビジョン\_1 構造、NDIS 6.30 Xxx がある場合に\_リビジョン\_2 構造体。

## <a name="related-topics"></a>関連トピック


[NDIS のバージョンの概要](overview-of-ndis-versions.md)

[NDIS バージョン情報を指定します。](specifying-ndis-version-information.md)

 

 






