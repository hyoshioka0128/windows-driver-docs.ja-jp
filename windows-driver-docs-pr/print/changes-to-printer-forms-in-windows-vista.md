---
title: Windows Vista のプリンター フォーム変更
description: Windows Vista のプリンター フォーム変更
ms.assetid: 6e970cbd-1c7f-4c48-8d05-a29f922a3f33
keywords:
- プリンタ フォーム WDK
- フォームの WDK プリンター
- 特殊な形式の WDK プリンター
- 特殊な用紙サイズの WDK プリンター
- WDK のフォームの用紙サイズします。
- カスタム フォームの WDK プリンター
- FORM_INFO_2 データ構造の WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e3d921e812651fddb5e6f5c98c1a1f73a90f6c3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347218"
---
# <a name="changes-to-printer-forms-in-windows-vista"></a>Windows Vista のプリンター フォーム変更


Windows Vista では、前にフォームはされたフォームのサイズと名前を使用して内部的に識別されます。 このメソッドは、ただし、常に動作しないも、プリント サーバーとクライアント コンピューターが別の言語にローカライズされたプリンター ドライバーを使用する場合。 Windows Vista では、印刷スプーラーが改善されプリンター ドライバーがクライアント コンピューターをサポートし、プリント サーバーを異なる言語にローカライズできるようにします。

Windows Vista は、フォームを追加します\_情報\_形式のスーパー セットである 2 つのデータ構造体\_情報\_にプリンター ドライバーを有効にする必要のある情報の追加メンバーを含む 1 つのデータ構造体。異なる言語でのシステムで機能します。

Unidrv プリンター ドライバーがフォームを使用する Windows Vista のアップグレードも\_情報\_2 つのデータ構造と GPD ファイルからデータを使用して、追加のメンバーを入力します。 フォームを使用しているモノリシックなプリンター ドライバーをアップグレードする\_情報\_フォームを使用する 1 構造\_情報\_新しい構造体を提供する追加情報が必要な場合、2 つ構造体。

このセクションでは、新しいメンバーを使用する、モノリシックなプリンター ドライバー、Unidrv プリンター ドライバーやコードの GPD ファイルを更新する方法について説明するフォーム\_情報\_2 のデータ構造を提供します。

このセクションでは、Windows Vista のプリンター フォームで次の機能強化について説明します。

[フォーム\_情報\_2 つのデータ構造体](form-info-2-data-structure.md)

[改善されたフォームをアルゴリズムに一致します。](improved-form-matching-algorithm.md)

[用紙トレイ照合アルゴリズムが強化されました](improved-form-to-tray-matching-algorithm.md)

詳細については、プリンター フォームを使用して、Microsoft Windows SDK のドキュメントを参照してください。

 

 




