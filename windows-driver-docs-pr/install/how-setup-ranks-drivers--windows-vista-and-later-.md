---
title: Windows のドライバーのランキング方法
description: Windows のドライバーのランキング方法
ms.assetid: 54b6f40a-e5f6-41dd-8876-c9f0fb36ee00
keywords:
- ドライバー WDK デバイスのインストールを順位付け
- ドライバーのランク WDK デバイスのインストール
- オプションのドライバー WDK デバイスのインストール、ドライバーのランク付け
- デバイス インストール WDK デバイス インストールの場合、ドライバーのランクのドライバーを検索します。
- WDK のデバイスのデバイスのインストール中にドライバーを検索
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3486ed018fcf84947682336fc87274459ce55b51
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386284"
---
# <a name="how-windows-ranks-drivers"></a>Windows のドライバーのランキング方法


Windows では、デバイスに一致するドライバーにランクを割り当てます。 ランクは、ドライバーがデバイスに一致する度合いを示します。 ドライバーのランクは 0 以上の整数で表されます。 ランク、一致するドライバーが高まりますが、デバイスは低くなります。

ドライバーのランクは、ドライバーとの間の一致の種類でサポートされている機能、ドライバーの署名に依存する複合値、[識別文字列](device-identification-strings.md)とデバイスのデバイスで報告します。識別文字列のエントリで指定されている、 [ **INF モデル セクション**](inf-models-section.md)のドライバーの INF ファイル。

ランクは、DWORD 型の値で表されます。 ランクは、署名のスコア付け、特徴のスコア、および識別子のスコア付けの合計です。 ランクは 0 x として書式設定*SSGGTHHH*ここで、 *S*、 *G*、 *T*、および*H* 4 ビット フィールドは、*SS*、 *GG*、および*THHH*フィールドは次のように、次の 3 つの順位付けのスコアを表します。

-   [署名スコア](signature-score--windows-vista-and-later-.md)ドライバーの署名が信頼されているかどうかに基づいて順位付けされます。 署名のスコアがの値のみに依存、 *SS*フィールド。 指定されていない署名のスコア付けは、0 x として表されます。*SS*0000000 します。

    Windows Vista と以降のバージョンの Windows の使用方法、ドライバーの署名、ドライバーをインストールする方法を決定するの概要については、次を参照してください。[署名カテゴリとドライバーのインストール](signature-categories-and-driver-installation.md)します。

-   [特徴スコア](feature-score--windows-vista-and-later-.md)ドライバーがサポートする機能に基づいたドライバーのランク付けします。 特徴のスコアがの値のみに依存、 *GG*フィールド。 指定されていない機能のスコア付けは、0x00 として表されます。*GG*0000 です。

-   [識別子スコア](identifier-score--windows-vista-and-later-.md)間の一致の種類に基づいたドライバーのランクを付け、[デバイス識別文字列](device-identification-strings.md)デバイスと、INF のエントリに記載されているデバイスの識別文字列によって報告されました。*モデル*ドライバーの INF ファイルのセクション。 識別子のスコアがの値のみに依存、 *THHH*フィールド。 指定されていない識別子のスコア付けは、0x0000 として表されます。*THHH*します。

ドライバーとドライバーの署名の種類のランクを示す SetupAPI ログのエントリについては、次を参照してください。 [SetupAPI ログ ドライバーのランク情報](driver-rank-information-in-the-setupapi-log.md)します。

 

 





