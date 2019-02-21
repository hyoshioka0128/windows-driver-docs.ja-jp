---
title: インジケーターの実装
description: このトピックでは、インジケーターの実装について説明します。
ms.assetid: 60BCE8C7-416E-4D5B-9B32-9B398CEA6A8A
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8c8774c64672b171c9e8e1825a0ce60ebdb1c5d9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559828"
---
# <a name="indicator-implementation"></a>インジケーターの実装

このトピックでは、インジケーターの実装について説明します。

センサーの配置と関連ロジックがシステムに固有であるためは、システムが、次のよう、関連する power 遷移を実行するときに、モードを更新します。

- コネクト スタンバイから出てくる
- スリープまたは休止状態の受信
- 起動後に

これにより、適切な状態を強制し、により、ユーザー インターフェイス層を更新します。

## <a name="laptopslate-mode---implementation-for-convertibles"></a>ラップトップ/スレート モード - コンバーチブルの実装

*図 1 に変換できる実装オプション*変換可能なシステムに GPIO インジケーターを実装するためのオプションが表示されます。

![変換可能な実装オプション](images/implementationconvertibles.jpg)

図 1 の変換可能な実装オプション

## <a name="laptopslate-mode---implementation-for-laptops"></a>ラップトップ/スレート モード - ラップトップの実装

*図 2 ラップトップ実装オプション*ラップトップ システムに GPIO インジケーターを実装するためのオプションが表示されます。

![ラップトップの実装オプション](images/implementationlaptops.jpg)

図 2 ラップトップ実装オプション

ConvertibleSlateMode[無人 Windows セットアップ](https://go.microsoft.com/fwlink/p/?linkid=276788)設定では、Oem にラップトップ モード フラグ clamshells 静的にするイメージのカスタマイズとして注入メカニズムを実装することがなく。

この機能は、(ユーザーは、いつでも使用できます) を完全に接続されているキーボードがタッチ スクリーン システムを対象とします。 ここでは、GPIO インジケーターを持たないタッチ スクリーン クラムシェル提供されている例では、/インジェクションを使用できます。

この設定は、特殊な構成パスの一部として適用する必要があり、すべての Windows クライアント オペレーティング システムに適用できます。 参照してください[識別無人セットアップ設定パス](http://sharepoint/sites/cba/Wiki Pages/Identifying Unattend Setting Passes.aspx)詳細についてはします。

コード サンプルを参照してください。

> [!NOTE]
> - GPIO ボタン ドライバーを読み込むには、無人セットアップ設定で導入される値よりも優先されます。
> - 注入メカニズムは、Windows 8.1 のシステムで使用できます。
> - 無人セットアップ設定を ConvertibleSlateMode Windows 8 は Windows 8.1 のアップグレード シナリオに影響しません。
> - 場合は、ConvertibleSlateMode 無人セットアップ設定が存在しないと GPIO インジケーターが実装されていません、スレート モードに、システムの既定値します。
> - ConvertibleSlateMode 無人設定を Windows Server オペレーティング システムをご利用いただけません。
