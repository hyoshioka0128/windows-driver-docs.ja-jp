---
title: WIA 項目に PTP オブジェクトのマッピング
description: WIA 項目に PTP オブジェクトのマッピング
ms.assetid: 3ee88c09-7f36-403a-ae7b-41d08c11c52f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96901a278a42459a96629486aec6f8dd0b0ab8bc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537454"
---
# <a name="mapping-ptp-objects-to-wia-items"></a>WIA 項目に PTP オブジェクトのマッピング





WIA 項目は、デバイス上に存在 PTP オブジェクトごとに作成されます。 ドライバーで報告されるように、同じ階層内のオブジェクトが表示されます。 たとえば、"XYZ"という名前のフォルダーの下のすべてのオブジェクトが報告された場合、画像が表示されますエクスプ ローラーで"XYZ"という名前のフォルダーの下。

このルールの 1 つの例外は、StorageInfo データセットで DCF としてその FilesystemType を報告するデバイスのです。 その場合は、最上位レベルのフォルダーには"DCIM"(存在する) 場合と呼ばれ、下のフォルダーの次のレベルは、Microsoft PTP クラスの WIA ミニドライバーによって隠されています。 すべてのサブフォルダーにあるオブジェクトは、最上位レベルに昇格されます。 ファイル名拡張子を (たとえば、します。JPG) は、WIA に送信される前にオブジェクトの名前から削除されます。

 

 




