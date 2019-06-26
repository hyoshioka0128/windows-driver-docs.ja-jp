---
title: Windows カーネルモード構成マネージャー
description: Windows カーネルモード構成マネージャー
ms.assetid: 0499121b-6f0b-464f-b422-610122fb7d3b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2d5afb5aa574b1a50f17eda4fb92ed4e03ff59b9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358065"
---
# <a name="windows-kernel-mode-configuration-manager"></a>Windows カーネルモード構成マネージャー


Microsoft Windows の以前の日、アプリケーションとオペレーティング システムは、"INI"(初期化) ファイル内の構成値を格納します。 これは、次の 1 つの Windows セッションから保持でした状態値を格納する簡単な方法を提供します。 ただし、Windows 環境が複雑になると、オペレーティング システムとアプリケーションについての永続的な情報を保存する新しいシステムが必要でした。 ハードウェアとソフトウェアに関するデータを格納する Windows レジストリが作成されました。

Windows カーネル モードの構成マネージャーでは、レジストリを管理します。 ドライバーは、レジストリの変更について知っておく必要がある場合、によって、特定のレジストリ データに対してコールバックを登録する configuration manager のルーチンを使用できます。 次に、レジストリ内のデータが変更されたときに、コールバックがトリガーされ、コールバック情報は、ドライバーを処理するコードを実行することができます。

Configuration manager への直接インターフェイスを提供するルーチンの文字が付いて"**Cm**"。 たとえば、 **CmRegisterCallback**します。 Configuration manager のルーチンの一覧は、次を参照してください。 [Configuration Manager ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

直接、構成マネージャーを呼び出し、その他の方法は、ドライバーのレジストリを操作することがあります。 詳細については、ドライバーのレジストリを使用して、次を参照してください。 [、ドライバーのレジストリを使用して](using-the-registry-in-a-driver.md)と[ドライバーのレジストリ キー](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-registry-trees-and-keys)します。

 

 




