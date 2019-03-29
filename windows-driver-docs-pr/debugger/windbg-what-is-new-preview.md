---
title: WinDbg プレビュー - 新機能
description: このトピックでは、新機能については WinDbg プレビュー デバッガーで inofmration を提供します。
ms.date: 05/23/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: medium
ms.openlocfilehash: 4cc2957dcd4ad25304c7dfa47e81425c9bd554aa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572166"
---
# <a name="windbg-preview---whats-new"></a>WinDbg プレビュー - 新機能

このトピックでは、新 WinDbg プレビュー デバッガーについてを説明します。 

デバッガーのリリースの詳細については、デバッガー ツール チームのブログを参照してください[ https://blogs.msdn.microsoft.com/windbg/](https://blogs.msdn.microsoft.com/windbg/)します。


## <a name="10120"></a>1.0.12.0

このバージョンは、WinDbg プレビューの最初のリリースでした。 WinDbg のプレビューで使用できる機能についての一般的な[WinDbg を使用してプレビューのデバッグ](debugging-using-windbg-preview.md)します。


## <a name="10130"></a>1.0.13.0

このバージョンでは、タイム トラベルのトレースを追加します。 時間、出張のデバッグ、プロセスを記録し、後で両方 forwards と backwards 再生することができます。 タイム トラベルのデバッグ (TTD) を使用することができるため、バグが見つかるまで、問題を再現するのではなく、デバッガー セッションを「巻き戻す」問題を簡単をデバッグできます。 詳細については、次を参照してください。[タイム トラベルのデバッグ - 概要](time-travel-debugging-overview.md)します。


## <a name="10140"></a>1.0.14.0

このバージョンには、これらの更新プログラムが含まれています。

- [デバッグ開始] ページには、リモートのプロセス サーバー (DbgSrv) に接続しているし、接続を切断することができるかどうかに表示されます。
- [表示] リボンの新しいレイアウトが事前設定されたオプションです。
- 新しいタイム トラベル リボン、時間をデバッグするときに、トレースを移動します。
- 多くの修正、更新、および JSProvider Api への変更は、詳細については、完全なリリース ノートを参照してください。

既知の問題
- X86 で動作しません SOS トレースします。


## <a name="11712150030"></a>1.1712.15003.0

このバージョンには、これらの更新プログラムが含まれています。

- TTD トレース内のメモリを照会できますようになりました
- 設定は WinDbg プレビュー セッション間で保持するようになりました
- 起動時のパフォーマンスの向上
- 追加のバグ修正

## <a name="10180418003"></a>1.0.1804.18003

このバージョンには、これらの更新プログラムが含まれています。

- シンボルの状態とキャンセルの機能強化
- 実験的なノート ウィンドウ
- 高速の実験用のソース ウィンドウ
- JSProvider API バージョン 1.2
- 軽微な変更とバグ修正


## <a name="10180517002"></a>1.0.1805.17002

このバージョンには、これらの更新プログラムが含まれています。

- 新しい [逆アセンブル] ウィンドウ
- 高速のソース ウィンドウ
- 軽微な変更とバグ修正

## <a name="10180711002"></a>1.0.1807.11002 

このバージョンには、これらの更新プログラムが含まれています。

- 自動保存とブレークポイントの読み込み
- 軽微な変更とバグ修正

## <a name="1018102001"></a>1.0.1810.2001 

このバージョンには、これらの更新プログラムが含まれています。

- [ファイル] メニューまたは [ホーム] リボンからアクセスされる新しい設定ダイアログ。 
- イベントと例外の設定 ダイアログ ボックス
- 優れたパフォーマンス向上の TTD インデクサー
- 新しい*debugArch*アーキテクチャを指定するためのフラグの起動
- 軽微な変更とバグ修正

---
 
## <a name="see-also"></a>関連項目


[https://blogs.msdn.microsoft.com/windbg/](https://blogs.msdn.microsoft.com/windbg/)

[WinDbg のプレビューを使用したデバッグ](debugging-using-windbg-preview.md)
 





