---
title: NDIS デバッグの準備
description: NDIS デバッグの準備
ms.assetid: 9a23cc3a-5940-46c3-928f-7fac46dfaba2
keywords:
- NDIS デバッグのセットアップ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7fbe07eac5153ee538c0bd540be3f6586b94d90
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535723"
---
# <a name="preparing-for-ndis-debugging"></a>NDIS デバッグの準備


NDIS コンポーネントをデバッグするには、ターゲット コンピューターに Ndis.sys のチェック済みバージョンが必要です。 ただし、全体のチェック ビルド オペレーティング システムをインストールする代わりに、それ以外の場合の無料のビルドのオペレーティング システムに Ndis.sys のチェック済みバージョンをコピーできます。 Ndis.sys のチェック済みバージョンをターゲット コンピューターにコピーする前に、Windows ファイル保護 (WFP) を無効にする必要があります。 WFP が無効になっていることを確認するには、セーフ モードでオペレーティング システムを起動します。

NDIS シンボルは、Microsoft のシンボル ストアで公開されています。 これにアクセスする方法の詳細については、[Microsoft パブリック シンボル](microsoft-public-symbols.md)を参照してください。

 

 





