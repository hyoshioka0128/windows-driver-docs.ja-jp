---
title: 接続して表示の構成
description: 接続して表示の構成
ms.assetid: 8c16f99e-c7fd-46e2-b102-f5f0a297fbec
keywords:
- Windows 7 の WDK の表示を表示します。
- WDK の Windows Server 2008 R2 の表示を表示します。
- 表示 WDK Windows 7 の表示、接続します。
- 表示 WDK Windows Server 2008 R2 の表示、接続します。
- 表示 WDK Windows 7 の表示、構成します。
- 表示 WDK Windows Server 2008 R2 の表示、構成します。
- WDK の Windows 7 のディスプレイの接続が表示されます。
- 接続には、WDK の Windows Server 2008 R2 の表示が表示されます。
- 構成するには、WDK Windows 7 の表示が表示されます。
- 構成するには、WDK Windows Server 2008 R2 の表示が表示されます。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 009254a44c1b873eea26023ec2ba5cc6c0dff709
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552576"
---
# <a name="connecting-and-configuring-displays"></a>接続して表示の構成


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Microsoft Windows オペレーティング システムにのみ適用されます。

新しい接続と記載されている構成が表示されます (CCD) Win32 Api [CCD Ddi](ccd-ddis.md)デスクトップ ディスプレイの設定をより細かく制御します。 アプリにも使用[縦デバイスで正しく表示](displaying-app-on-portrait-device.md)します。 たとえば、Windows 7 よりも前の Windows のバージョンでは、できなかった複製モードを使用して設定する、 **ChangeDisplaySettingsEx**関数。 ビュー名のように、および Windows グラフィックス デバイス インターフェイス (GDI) の概念を使用してから、新しい CCD Api を移動[Windows Display Driver Model (WDDM)](windows-vista-display-driver-model-design-guide.md)概念などのアダプター、ソース、およびターゲットの識別子。

コントロール パネルの 画面、新しいホット キー、およびホット プラグ検出 (HPD) マネージャーでは、CCD Api を使用できます。 Oem の CCD Api を使用して、付加価値アプレット プライベート ドライバー エスケープを使用する代わりにします。

CCD Api では、次の機能を提供します。

-   現在接続されている表示可能な表示パスを列挙します。

-   トポロジを設定します (たとえば、複製し、拡張、) のレイアウト情報、解像度、向き、および 1 つの関数の呼び出しで接続されているすべてのディスプレイの縦横比。 1 つの関数の呼び出しで接続されているすべてのディスプレイの複数の設定を実行して、画面の点滅の数が減少します。

-   追加または、永続性データベースへの設定を更新します。

-   データベースに保持されている設定を適用します。

-   最適なモードのロジックを使用して、最適な表示設定を適用します。

-   最適なトポロジのロジックを使用すると、接続されるディスプレイの最適なトポロジを適用できます。

-   開始または停止は、出力を強制します。

-   新しいオペレーティング システムの永続性データベースを使用する OEM のホット キーを使用できます。

CCD Api は、次のタスクを処理できません。 さらに、CCD Api でないとの下位互換性、 [Windows 2000 のディスプレイ ドライバー モデル](windows-2000-display-driver-model-design-guide.md)します。

-   API のセットを交換し、プライベートのドライバーは、ハードウェア ベンダーのコントロールのデスクトップに提供されていたディスプレイの設定をエスケープします。

-   カーネル モードのディスプレイのミニポート ドライバーにプライベート データを渡します。

-   新しいモニター コントロール Api のセットを提供します。

-   EDID、DDCCI は、monitor の機能のクエリを実行します。

-   CCD Api は、永続性データベースから取得する設定を一意に識別するコンテキスト id を提供します。

-   CCD Api では、呼び出し元を取得および表示を設定できますが、指定されたパスの可能性のあるソース モードを列挙する機能は提供されません。 Windows 7 を既に前から存在している Api は、この機能を提供します。

次のセクションでは、さらに詳しく CCD Api について説明します。

[CCD 概念](ccd-concepts.md)

[CCD Api](ccd-apis.md)

**注**  に加えて CCD Api を使用して、デスクトップでの表示を設定する、ハードウェア ベンダーが、Windows 7 を変更する必要があります [Windows 表示 Driver Model (WDDM)](windows-vista-display-driver-model-design-guide.md)サポート CCD ミニポート ドライバーを表示します。 ディスプレイのミニポート ドライバーで CCD のサポートに関する詳細については、[CCD Ddi](ccd-ddis.md)を参照してください。

 

 

 





