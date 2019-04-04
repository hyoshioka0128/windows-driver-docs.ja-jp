---
title: Windows カーネル モードの Configuration Manager
description: Windows カーネル モードの Configuration Manager
ms.assetid: 0499121b-6f0b-464f-b422-610122fb7d3b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 074f89e6b4dd93398e6d64fb3a624d89466fe73c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529947"
---
# <a name="windows-kernel-mode-configuration-manager"></a>Windows カーネル モードの Configuration Manager


Microsoft Windows の以前の日、アプリケーションとオペレーティング システムは、"INI"(初期化) ファイル内の構成値を格納します。 これは、次の 1 つの Windows セッションから保持でした状態値を格納する簡単な方法を提供します。 ただし、Windows 環境が複雑になると、オペレーティング システムとアプリケーションについての永続的な情報を保存する新しいシステムが必要でした。 ハードウェアとソフトウェアに関するデータを格納する Windows レジストリが作成されました。

Windows カーネル モードの構成マネージャーでは、レジストリを管理します。 ドライバーは、レジストリの変更について知っておく必要がある場合、によって、特定のレジストリ データに対してコールバックを登録する configuration manager のルーチンを使用できます。 次に、レジストリ内のデータが変更されたときに、コールバックがトリガーされ、コールバック情報は、ドライバーを処理するコードを実行することができます。

Configuration manager への直接インターフェイスを提供するルーチンの文字が付いて"**Cm**"。 たとえば、 **CmRegisterCallback**します。 Configuration manager のルーチンの一覧は、[Configuration Manager ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff542038)を参照してください。

直接、構成マネージャーを呼び出し、その他の方法は、ドライバーのレジストリを操作することがあります。 詳細については、ドライバーのレジストリを使用して、[、ドライバーのレジストリを使用して](using-the-registry-in-a-driver.md)と[ドライバーのレジストリ キー](https://msdn.microsoft.com/library/windows/hardware/ff549538)を参照してください。

 

 




