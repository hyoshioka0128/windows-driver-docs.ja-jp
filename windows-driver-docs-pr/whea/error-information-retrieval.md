---
title: エラー情報の取得
description: エラー情報の取得
ms.assetid: 4af06727-9660-4bbc-8c9e-a50c8f2d566d
keywords:
- Windows ハードウェア アーキテクチャ WDK のエラー、エラー情報の取得
- WHEA WDK、エラー情報の取得
- ハードウェア エラー WDK WHEA、エラー情報の取得
- WDK WHEA、エラー情報の取得エラー
- プラットフォーム固有のハードウェア エラー ドライバー プラグインを WDK WHEA、エラー情報の取得
- PSHED プラグイン WDK WHEA、エラー情報の取得
- WDK WHEA エラー情報の取得
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 143d8296c23015bbc52052dcdf88c2d124dd1a06
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354456"
---
# <a name="error-information-retrieval"></a>エラー情報の取得


ハードウェアのエラー状態の処理中にエラー処理プロセスの 3 つの独立した時点で、PSHED が呼び出されます。

-   低レベル ハードウェア エラー ハンドラー (LLHEH) は、LLHEH がオペレーティング システムにエラーを報告する前に、エラー条件に関する補足情報をハードウェアのエラー パケットに追加できるように、PSHED に呼び出します。

-   Windows カーネルは、エラー状態を説明するエラー レコードに補助エラー レコード セクションに追加できるように、PSHED を呼び出します。

-   修正されたエラーは、it がエラーの発生元のエラー状態をクリアするよう PSHED にカーネルの呼び出しを登録、エラーの処理が Windows を実行します。

PSHED、PSHED を検出する標準的なエラーのソースによって報告されるエラー条件のエラー情報の取得操作をサポートしています。 参加しているプラグイン PSHED が実装されている場合[エラー ソースの検出](error-source-discovery.md)とレポートのプラグインの PSHED、PSHED をサポートしていないオペレーティング システムに追加のエラーのソースは、エラー情報にも参加する必要がありますこれらのエラーのソースのエラー情報の取得操作をサポートするために取得します。 PSHED のプラグインは、標準エラーのソースによって報告されるエラー条件に対して追加のエラー情報を提供するエラー情報の取得も参加できます。

**注**  に参加する必要がありますエラー情報の取得に参加しているプラグイン A PSHED[エラー ソースの検出](error-source-discovery.md)次のいずれかが true の場合。
-   PSHED プラグインは、特定のエラーのソースによって報告されるハードウェアのエラー パケットに追加のエラー情報を提供します。 このような状況では、プラグインの PSHED に含まれている値を変更する必要があります、 **MaxRawDataLength**のメンバー、 [ **WHEA\_エラー\_ソース\_記述子** ](https://msdn.microsoft.com/library/windows/hardware/ff560505)追加のエラー情報に対応するエラーのソースの検出中にそのエラーの発生元の構造体。

-   PSHED プラグインは、特定のエラーのソースによって報告されるハードウェア エラーのエラー レコードをレコードのセクションで追加のエラーを提供します。 このような状況では、プラグインの PSHED に含まれている値を変更する必要があります、 **MaxSectionsPerRecord** WHEA のメンバー\_エラー\_ソース\_エラー ソースの記述子構造体追加のエラー レコードのセクションでは、対応するエラー ソースの検出中に。

 

エラー情報の取得に参加している PSHED プラグインを実装する方法の詳細については、次を参照してください。[エラー情報の取得に参加している](participating-in-error-information-retrieval.md)します。

 

 




