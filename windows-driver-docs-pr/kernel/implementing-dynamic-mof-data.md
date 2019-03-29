---
title: 動的 MOF データの実装
description: 動的 MOF データの実装
ms.assetid: 408c0f64-6257-4ece-bb4d-b1850f8ae3c6
keywords:
- WMI の WDK カーネルでは、スキーマの公開
- 発行の WMI スキーマ WDK
- 発行 WDK WMI スキーマ
- MOF ファイルの WDK WMI
- 動的 MOF データ WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd436a85f6532977bdda64bad6a7d5411ff9eb30
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574432"
---
# <a name="implementing-dynamic-mof-data"></a>動的 MOF データの実装





ドライバーのスキーマは、実行時に、ドライバーのバイナリと戻り値の選択したスキーマ情報] の [MOF のバイナリ データを含めることによって動的に公開できます。 動的 MOF データを指定するには、ドライバーは以下の手順を実行する必要があります。

1.  」の説明に従って、MOF ファイルをコンパイル[ドライバーの MOF ファイルをコンパイルする](compiling-a-driver-s-mof-file.md)します。

2.  MOF コンパイラによって作成された .bmf ファイルの 16 進ダンプが含まれる .x ファイルを作成するのにには、wmimofck.exe を使用します。

3.  使用**\#含める**ドライバーのソースと手順 2. で作成された 16 進数のデータを含めます。

4.  MSWmi のサポートとして登録\_MofData\_GUID は、予測で定義されている guid。

5.  WMI を両方への応答で選択したバイナリ データを返す、 [ **IRP\_MN\_クエリ\_すべて\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff551650)または[ **IRP\_MN\_クエリ\_単一\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff551718) MSWmi 要求\_MofData\_GUID。

Wmimofck ユーティリティの詳細については、次を参照してください。 [wmimofck.exe を使用して](using-wmimofck-exe.md)します。

 

 




