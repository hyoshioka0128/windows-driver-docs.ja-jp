---
title: カーネル モードのパフォーマンス カウンターについて
description: カーネル モードのパフォーマンス カウンターについて
ms.assetid: 57655e65-6db4-487d-8831-282e8d30d84e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80fce5d09c2d60eaa2432de0a89d5eb2f2d74990
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769422"
---
# <a name="about-kernel-mode-performance-counters"></a>カーネル モードのパフォーマンス カウンターについて


Windows のパフォーマンスカウンター (PCW) は、システム内のさまざまなコンポーネントとやり取りし、カーネルモードコンポーネントによって提供されるカウンターセット (およびそのインスタンス) を追跡します。 また、PCW は、カウンターセットを確認し、要求されたデータを返すことによって、コンシューマーからのサービス要求を追跡します。

カーネルモードの PCW プロバイダーは、システムのパフォーマンスカウンターライブラリ (PERFLIB) (バージョン2プロバイダー) としてインストールされます。これにより、カウンターを参照し、データの収集とインスタンスの列挙を行うことができます。 コンシューマーは、コンシューマーコードに変更を加えることなく、PDH および PERFLIB バージョン1を使用して、KM PCW プロバイダーに対してクエリを実行できます。 詳細については、「[パフォーマンスカウンター](https://docs.microsoft.com/windows/win32/perfctrs/performance-counters-portal)」を参照してください。

カーネルモードで実行されているプロバイダーは、カーネルモードの PCW provider API を使用してカウンターセットを登録します。 プロバイダーは、登録されているカウンターセットのインスタンスを管理し、パフォーマンスカウンターに関連するさまざまなイベントが発生したときに通知を受け取ることができます (コンシューマーがカウンターを追加、削除、収集する場合など)。

**メモ**   Windows 7 で導入されたカーネルモードの PCW provider API (PERFLIB バージョン 2) では、現在、セッションスペースドライバーはサポートされていません。

 

 

 





