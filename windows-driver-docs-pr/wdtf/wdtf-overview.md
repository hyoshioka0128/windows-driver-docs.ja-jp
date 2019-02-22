---
title: WDTF アーキテクチャと概要
description: Microsoft Windows デバイスのテスト フレームワーク (WDTF) を使用して作成、管理、再利用、およびデバイスを中心とした、シナリオ ベースの自動テストを拡張する方法について説明します。
ms.assetid: 7e7660ec-1f17-4987-82c0-f62cca3a99b9
keywords:
- Windows デバイスのテスト フレームワーク WDK
- WDTF WDK
- WDK WDTF スクリプト
- Windows デバイスのテスト フレームワークに関する WDTF の WDK
- Windows デバイスのテスト フレームワークに関する、WDTF WDK
- テスト スクリプト WDK WDTF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50b80966ab530d1d58eff813e3087390638b7667
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557825"
---
# <a name="wdtf-architecture-and-overview"></a>WDTF アーキテクチャと概要


Microsoft Windows デバイスのテスト フレームワーク (WDTF) を使用すると、作成、管理、再利用、およびデバイスを中心とした、シナリオ ベースの自動テストを拡張できます。

次の図に非常に大まかなシナリオを作成するための一般的な WDTF モデルを示します。

![非常に高いレベルでのシナリオを作成するための一般的な wdtf モデルを示す図 ](images/wdtf-scenariomodel.gif)

テスト スクリプトは、コンポーネント オブジェクト モデル (COM) インターフェイスを介して WDTF オブジェクトを使用します。 これらのシナリオを記述する COM オートメーションをサポートする任意のプログラミング言語を使用することができます。 このドキュメントでは、VBScript、C++、および JScript でのコード例を提供します。

さらに、コードを追加せず、WDTF サンプルを通じて、Driver Test Manager (DTM) を使用できます。

**注**  DTM の一部である、 [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?linkid=254893)と Microsoft Windows Logo Kit (WLK)。 DTM で WDTF ベースのテストを実行すると WDTF はインストールされます。

 

前の図は、個々 のデバイスではなくデバイスのグループの一般的な機能を集中できるようにする、コンポーネント ベースのシナリオを作成するためのモデルを示しています。 場合でも、多くのデバイスでは、これらのインターフェイスの一部の特殊な実装が必要なこれらは非常に簡単に追加できます。 ときに、シナリオでは、新しい機能を使用して、[追加](extending-the-framework.md)WDTF にその機能をラップする単純な COM オートメーション インターフェイス。

## <a name="in-this-section"></a>このセクションの内容


-   [WDTF アーキテクチャ](wdtf-architecture.md)
-   [フレームワークを拡張します。](extending-the-framework.md)

 

 




