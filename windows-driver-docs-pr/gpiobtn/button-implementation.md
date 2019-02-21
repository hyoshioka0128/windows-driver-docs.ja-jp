---
title: ボタンの実装
description: ボタンと状態インジケーターの両方の物理 GPIO リソースを使用することをお勧めします。
ms.assetid: ECF0723A-1AF0-4608-88CC-6ACBD98DA03C
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9d77ef895fd5ed00f5b29736fc9edd563e16d80e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532070"
---
# <a name="button-implementation"></a>ボタンの実装


ボタンと状態インジケーターの両方の物理 GPIO リソースを使用することをお勧めします。

システムに必須/任意のハードウェア ボタンまたは GPIO のインジケーター (ラップトップ/スレート モードを示す値または固定を示す値) の物理の GPIO リソースがないのでは、ユーザー モードまたはカーネル モード ドライバーが、受信トレイのドライバーの代わりに直接ビューステートの変更を挿入することができます。ボタン配列のデバイスに起因する物理ハードウェア リソース (\_CID PNP0C40)、ラップトップ/スレート モード状態インジケーター (\_CID PNP0C60) またはドッキング状態インジケーター (\_CID PNP0C70)。

インターフェイスを使用するには、エントリは、各インターフェイスが使用されるそれぞれのデバイスを定義する ACPI テーブルに存在する必要があります。 ただし、デバイスのすべての GPIO リソースの存在は省略可能です。 参照してください[ACPI 記述子サンプル](acpi-descriptor-samples.md)します。

 

 




