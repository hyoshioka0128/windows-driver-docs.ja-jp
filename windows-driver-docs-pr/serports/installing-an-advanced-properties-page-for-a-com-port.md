---
title: COM ポート用の詳細プロパティ ページをインストールする
description: COM ポート用の詳細プロパティ ページをインストールする
ms.assetid: 056fd245-a9d2-4a10-9e92-fe75e51f6770
keywords:
- 高度な COM ポートのプロパティ ページの WDK シリアル デバイス
- COM ポートの WDK シリアル デバイス
- COM ポートの既定のユーザー ダイアログ ボックス
- 既定値 ダイアログ ボックスの WDK シリアル デバイスをオーバーライドします。
- ポート番号の WDK シリアル デバイス
- FIFO 制御パラメーター WDK シリアル デバイス
- COM ポート番号の WDK シリアル デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bf067b86d74cb08382ec17a9d9beb58f2d0efdc
ms.sourcegitcommit: 6a0636c33e28ce2a9a742bae20610f0f3435262c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2019
ms.locfileid: "65836360"
---
# <a name="installing-an-advanced-properties-page-for-a-com-port"></a>COM ポート用の詳細プロパティ ページをインストールする

高度なプロパティ ページには、FIFO 制御パラメーターを設定し、COM ポート番号を選択するための既定のユーザー ダイアログ ボックスが表示されます。 ただし、カスタム ダイアログ ボックスを指定することで、[既定] ダイアログ ボックスをオーバーライドできます。

COM ポートのシステム提供のプロパティ ページと既定のダイアログ ボックスをインストールするには、次の操作を行います。

1. Microsoft Win32 プロパティ ページのプロバイダーを実装します。 プロパティ シートのダイアログ ボックスのインストールの概要については、次を参照してください。[デバイスのプロパティ ページを提供する](https://msdn.microsoft.com/library/windows/hardware/ff549784)します。

    プロパティ ページのプロバイダーを呼び出して、システムが提供[ **SerialDisplayAdvancedSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff547447)ルーチンで、既定のシステム提供のダイアログ ボックスが表示されます。

2. 設定して、プロパティ ページのプロバイダーをインストール、 **EnumPropPages32**内のエントリの値、*追加レジストリ セクション*はデバイスのによって参照される[ **DDInstall セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344). 説明を参照して、 **EnumPropPages32**内のエントリの値[ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)します。

によって表示される既定のダイアログ ボックスをオーバーライドする**SerialDisplayAdvancedSettings**次の操作を行います。

1. カスタム ダイアログを実装*DLL*します。 ダイアログ ボックスのエントリ ポイントは、 [**サポート\_[詳細設定]\_ダイアログ**](https://msdn.microsoft.com/library/windows/hardware/ff546956)-ルーチンを入力します。

2. 設定して、カスタム ダイアログ DLL をインストール、 **EnumAdvancedDialog**エントリの値で、*追加レジストリ セクション*はデバイスのによって参照される[ **DDInstall セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344). 種類と値のエントリの形式を使用すると同じ、 **EnumPropPages32**エントリの値します。
