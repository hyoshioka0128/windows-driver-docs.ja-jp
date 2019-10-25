---
title: ALE エンドポイント有効期間管理
description: ALE エンドポイント有効期間管理
ms.assetid: cbf54062-4ced-4cf6-babf-e9e4e1ddf302
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de81b2413b85e23d8bed928ea1cced6c5bfd541f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835387"
---
# <a name="ale-endpoint-lifetime-management"></a>ALE エンドポイント有効期間管理


アプリケーションレイヤー強制 (ALE) をサポートするコールアウトドライバーでは、プロセスの兆候にリソースを割り当てる必要がある場合があります。 このトピックでは、関連するエンドポイントが閉じられたときに、このようなリソースを解放するようにコールアウトドライバーを構成する方法について説明します。 ALE エンドポイントの有効期間の管理は、windows 7 以降のバージョンの Windows でサポートされています。

ALE エンドポイントに関連付けられているリソースを管理するために、コールアウトドライバーは次のレイヤーに登録できます。

-   FWPS\_レイヤー\_ALE\_RESOURCE\_RELEASE\_V4 (FWPM\_LAYER\_ALE\_RESOURCE\_RELEASE\_V4)

-   FWPS\_レイヤー\_ALE\_リソース\_リリース\_V6 (FWPM\_LAYER\_ALE\_RESOURCE\_RELEASE\_V6)

-   FWPS\_レイヤー\_ALE\_エンドポイント\_クロージャ\_V4 (FWPM\_LAYER\_ALE\_ENDPOINT\_クロージャ\_V4)

-   FWPS\_レイヤー\_ALE\_エンドポイント\_クロージャ\_V6 (FWPM\_LAYER\_ALE\_ENDPOINT\_クロージャ\_V6)

ALE リソース解放レイヤーは、対応する ALE リソース割り当てレイヤーに示されるたびに表示されます (たとえば、FWPS\_レイヤー\_ALE\_リソース\_割り当て\_V4)。 コールアウトドライバがリリースレイヤーと割り当てレイヤーを確実に一致させるには、FWPS\_METADATA\_FIELD\_TRANSPORT\_ENDPOINT\_HANDLE metadata フィールドを両方のレイヤーに指定し、各エンドポイントに一意のが割り当てられていることを確認します。扱え.

ALE エンドポイントのクロージャレイヤーは、エンドポイントの種類に応じて異なる方法で呼び出されます。 TCP 接続の場合は、すべての ALE 承認接続レイヤー (たとえば、FWPS\_レイヤー\_ALE\_AUTH\_CONNECT\_V4) または ALE 承認 receive accept レイヤー (FWPS\_レイヤーなど) に対して、ALE エンドポイントクロージャが示されます。\_ALE\_AUTH\_受信\_\_V4) の通知を受け取ります。 ALE リソースのリリースを示すように、エンジンはエンドポイントごとに一意のハンドルを割り当てて、FWPS\_メタデータ\_フィールド\_トランスポート\_エンドポイント\_のメタデータフィールドに渡します。 TCP 以外のエンドポイントについては、ソケットが通信する一意のリモートピアの数に関係なく、各エンドポイントに対して ALE エンドポイントクロージャレイヤーが呼び出されます。 また、各 TCP リスニングソケットに対しても、ALE エンドポイントクロージャレイヤーが呼び出されます。

ALE エンドポイントクロージャレイヤーに登録されているコールアウトは分類を保留できます。 これにより、コールアウトは、エンドポイントがシャットダウンされる前に、非同期処理のためにキューに入れられたすべてのパケットを reinject できます。 分類を保留するには、処理が完了したら、コールアウトドライバーが[**FwpsPendClassify0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpspendclassify0)を呼び出し、その後に[**FwpsCompleteClassify0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscompleteclassify0)を呼び出す必要があります。

適用可能な場合、エンジンは、FWPS\_メタデータ\_フィールド\_親\_エンドポイント\_メタデータフィールドの親エンドポイントの一意のハンドルを示します。 これにより、必要に応じて、コールアウトドライバーが親子関係を追跡できるようになります。

 

 





