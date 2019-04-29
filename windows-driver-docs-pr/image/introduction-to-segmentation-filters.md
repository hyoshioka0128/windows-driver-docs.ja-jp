---
title: セグメンテーション フィルターの概要
description: セグメンテーション フィルターの概要
ms.assetid: 3f73aa08-c3ef-4e97-9e3e-a1f0325cd599
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec74a5e0932326c049c8735c343cdb5b1239050f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327065"
---
# <a name="introduction-to-segmentation-filters"></a>セグメンテーション フィルターの概要





セグメント化フィルターは、個々 のフラット ベッド スキャナーでレイアウトされるため、個別のイメージを取得したこれらの画像の各画像を分離するアプリケーションで使用できる、WIA 拡張機能です。 セグメント化、フィルターは、アプリケーションのプロセスで実行されている、インプロセス COM コンポーネントです。

セグメント化フィルターが拡張するドライバーに依存します。 独自のセグメント化フィルターを記述したり、マイクロソフトが Windows Vista 以降を提供しているセグメント化フィルターを使用するドライバー開発者向けを選択できます。

セグメント化、フィルターは、サポートするアプリケーションでのみ使用できます、 [IStream ベース WIA 転送モデル](wia-transfer-architecture.md)します。

次の図は、アプリケーションのプロセスで実行中のセグメント化フィルター コンポーネントを示します。

![アプリケーションのプロセスで実行されている、セグメント化フィルター コンポーネントを示す図](images/wia-components-app-process.png)

 

 




