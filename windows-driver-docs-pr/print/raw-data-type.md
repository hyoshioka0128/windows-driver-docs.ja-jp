---
title: 生のデータ型
description: 生のデータ型
ms.assetid: f53264c1-97aa-42f0-8bab-76bf984f2c79
keywords:
- プリント プロセッサ WDK、データ型
- WDK のデータ型のプリント プロセッサ
- 生のデータ型の WDK のプリント プロセッサ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06427b130d4960d932e6b992292d599243b84d30
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548970"
---
# <a name="raw-data-type"></a>生のデータ型





生データは、さらに処理することがなく、印刷のモニターに送信できます。 プリント プロセッサは、スプーラーにこのデータを送信するだけ (呼び出して**WritePrinter**Microsoft Windows SDK ドキュメントで説明)、フィード形式を挿入することがあります。 未加工のデータ ファイルの例は、いずれかで構成される*プリンター制御言語 (PCL)* コマンド。 印刷ジョブがクライアントからサーバーに送信 RAW 形式で、クライアントまたはサーバーのいずれかが NT-ベースのオペレーティング システムの EMF をサポートしていない場合、またはサーバー管理者が EMF サポートを無効にした場合。 このような場合は、ジョブがサーバーに送信される前に、イメージのレンダリングがクライアントで実行します。

ターゲットのプリンタは、Postscript をサポートしている場合により、postscript コマンドに生データを検討できます。 その一方で、Sfmpsprt.dll プリント プロセッサは Postscript を入力し、非 Postscript プリンターを解釈します。 そのためその場合は、Postscript が生データ

生データの種類に関する詳細については、次を参照してください。、 *Windows 2000 Professional リソース キット*または*Windows 2000 Server Resource Kit*します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

 

 




