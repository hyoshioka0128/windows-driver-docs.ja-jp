---
title: ドライバーのテストとデバッグ用のブート オプション変更ツール
description: ドライバーのテストとデバッグ用のブート オプション変更ツール
ms.assetid: 4fd58868-7a43-42e3-adf9-5a82593c1675
keywords:
- ツールを WDK、ブート オプション
- ドライバーの開発ツールを WDK、ブート オプション
- WDK のブート オプション
- ドライバー WDK ブート オプションをテストします。
- テスト ドライバー WDK ブート オプション
- ドライバー WDK ブート オプションのデバッグ
- ドライバー WDK ブート オプションのデバッグ
- WDK のオペレーティング システムのブート オプション
- WDK のブート オプションの構成を読み込む
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: b4f8e49a6af8cf8da041fb8bb347c93988febf5e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572623"
---
# <a name="tools-for-changing-boot-options-for-driver-testing-and-debugging"></a>ドライバーのテストとデバッグ用のブート オプション変更ツール

テストして、Microsoft Windows オペレーティング システム上のドライバーをデバッグを有効にして、オペレーティング システムの読み込み時に確立されている機能を構成する必要があります。 これらの機能の設定が含まれている、*ブート オプション*--ブート ローダーの読み込みし、オペレーティング システムとその他の起動可能なプログラム、およびデバイスの構成を決定する値。

> [!TIP] 
> Windows Driver Kit (WDK) 8 を使用している場合は、テストと、Visual Studio からデバッグ用のコンピューターを構成できます。 テスト コンピューターを構成すると、WDK ドライバー テスト フレームワークは自動的にテスト コンピューターのリモート デバッグを有効にして、必要なテスト バイナリとサポート ファイルを転送します。 詳細については、次を参照してください[ドライバーの展開のためにコンピューターをプロビジョニングし、テスト (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)、または[ドライバーの展開のためにコンピューターをプロビジョニングし、テスト (WDK 8)](https://msdn.microsoft.com/library/windows/hardware/hh698272)、および[にドライバーをテストする方法。Visual Studio を使用してランタイム](https://docs.microsoft.com/windows-hardware/drivers/develop/testing-a-driver-at-runtime)します。

このセクションでは、追加、削除、およびオペレーティング システムの負荷の新しい構成を作成するためのブート オプションを変更する方法と、ブート エントリのパラメーターを使用して、ドライバーのテストとデバッグの構成をロードをカスタマイズする方法について説明します。

ブート オプションを編集するには、次の操作を実行できます。

- 有効にして、デバッグの構成

- 特定のカーネル、またはハードウェア アブストラクション レイヤー (HAL) ファイルを読み込む

- Windows で使用できる物理メモリを制限します。

- 有効化、無効にする、および 32 ビット バージョンの Windows の物理アドレス拡張 (PAE) を構成します。

- 非常に小さなカーネル モード アドレス空間でドライバーをテストする (3 GB) のユーザー モードとカーネル モード コンポーネント間の仮想アドレス空間を配分します。

- 有効にして構成データ実行防止 (/noexecute)

- ヘッドレス サーバーでコンソール リダイレクトを緊急管理サービス (EMS) 用のポートを指定します。

- 読み込まれるドライバーの名前を表示します。

このセクションの内容:

- [ブート オプションの概要](introduction-to-boot-options.md)
- [ブート オプションの編集](editing-boot-options.md)
- [Boot.ini のブート パラメーター参照](https://msdn.microsoft.com/library/windows/hardware/ff542248)
- [BCD のブート オプション リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff542205)
- [ブート パラメーターを使用します。](using-boot-parameters.md)
- [バイパスのブート オプション](bypassing-boot-options.md)

Windows Vista 以降、Windows には、新しいブート ローダーのアーキテクチャ、新しいブート オプション、および新しいブート オプション エディターが含まれます。 詳しくは、次を参照してください。 [Windows Vista のブート オプション](boot-options-in-windows-vista-and-later.md)します。
