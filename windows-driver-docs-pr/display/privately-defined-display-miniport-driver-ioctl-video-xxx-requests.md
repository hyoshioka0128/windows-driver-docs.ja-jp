---
title: プライベート ディスプレイ ミニポート ドライバー IOCTL_VIDEO_XXX 要求
description: それに対応するためのプライベートな I/O 制御コードは、ドライバーを表示またはミニポート ドライバーは、いずれかを定義できます。
ms.assetid: 45d8c9bc-993c-4fd3-949d-dfb30bb685d7
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000、要求の処理
- 要求処理の WDK ビデオのミニポート
- 非公開で定義されている IOCTL_VIDEO_XXX 要求 WDK ビデオのミニポート
- IOCTL_VIDEO_XXX 要求 WDK のビデオのミニポート
- I/O WDK ビデオのミニポート
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 2c538119d32d2ee98eaf40b7d6b9a6447b243728
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559563"
---
# <a name="privately-defined-display-miniport-driver-ioctlvideoxxx-requests"></a>表示ミニポート ドライバー IOCTL を個別に定義されている\_ビデオ\_XXX 要求

それに対応するためのプライベートな I/O 制御コードは、ドライバーを表示またはミニポート ドライバーは、いずれかを定義できます。

ただし、特定の表示-ミニポート ドライバー ペアのみでは、非公開で定義されている I/O 制御コードを使用できます。 つまり、既存のディスプレイ ドライバーで実行するように設計ミニポート ドライバー定義しないでくださいプライベート I/O 制御コード書き直されてないと、場合によっては既存の互換性に影響することがなく、既存のディスプレイ ドライバーは新しい I/O 制御要求を行うことはできませんので、ミニポート ドライバーが既に使用しています。 また、既存のまたは一般的なディスプレイ ドライバー、SVGA アダプターなどのアダプターの多くの異なるモデルの上層には、すべて基になるミニポート ドライバーに同じ効果が非公開で定義されている I/O 制御コードを使用できません。

プライベートの I/O の定義の詳細については、制御コードを参照してください[I/O 制御コードを使用して](https://msdn.microsoft.com/library/windows/hardware/ff565406)します。

 

 





