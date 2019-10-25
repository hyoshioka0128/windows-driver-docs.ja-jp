---
title: Windows カーネルモード構成マネージャー
description: Windows カーネルモード構成マネージャー
ms.assetid: 0499121b-6f0b-464f-b422-610122fb7d3b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7dbae31bc252300f1e62abdf27b5f869e4cfd42d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838309"
---
# <a name="windows-kernel-mode-configuration-manager"></a>Windows カーネルモード構成マネージャー


Microsoft Windows の以前のバージョンでは、アプリケーションとオペレーティングシステムによって構成値が "INI" (初期化) ファイルに格納されていました。 これにより、Windows セッション間で保持される可能性のある状態値を格納する簡単な方法が提供されました。 ただし、Windows 環境がより複雑になったため、オペレーティングシステムとアプリケーションに関する永続的な情報を格納する新しいシステムが必要でした。 Windows レジストリは、ハードウェアとソフトウェアに関するデータを格納するために作成されました。

Windows カーネルモード構成マネージャーは、レジストリを管理します。 ドライバーがレジストリの変更について認識する必要がある場合、特定のレジストリデータにコールバックを登録することによって、構成マネージャーのルーチンを使用することができます。 次に、レジストリ内のデータが変更されると、コールバックがトリガーされ、コードを実行して、ドライバー内のコールバック情報を処理できます。

構成マネージャーに直接インターフェイスを提供するルーチンには、先頭に文字 "**Cm**" が付いています。たとえば、 **Cmregistercallback**です。 Configuration manager ルーチンの一覧については、「 [Configuration Manager ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

構成マネージャーを直接呼び出すだけでなく、ドライバーでレジストリを操作する方法もあります。 ドライバーでのレジストリの使用の詳細については、「ドライバー[でのレジストリの使用](using-the-registry-in-a-driver.md)」および「[ドライバーのレジストリキー](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-registry-trees-and-keys)」を参照してください。

 

 




