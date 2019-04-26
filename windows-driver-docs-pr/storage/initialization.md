---
title: 初期化
description: 初期化
ms.assetid: 7d5ee1c7-df6c-4394-9ba7-819ee7e9397b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 551c1446fa8bbc87651cfe99d1e896b14d735d40
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359208"
---
# <a name="initialization"></a>初期化


LSI\_U3 Storport ミニポート ドライバーのエントリ ポイントが DriverEntry ルーチンで初期化されます。 その他の重要な初期化ルーチン LsiU3HWInitialize、LsiU3FindAdapter です。 後者の場合、ドライバーの同期モデルに設定されて*StorSynchronizeFullDuplex*、以前の要求が終了中に新しい要求を受信できるドライバーを意味します。 つまり、その可能性がありますが同時にキューの Storport から新しい要求を以前の要求に非同期的に実行中。

 

 




