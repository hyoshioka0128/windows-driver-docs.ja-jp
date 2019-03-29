---
title: MBR2GPT ツール テスト ガイダンス
description: MBR2GPT ツール テスト ガイダンス
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 434cf876f6e88e7a913a3acad2e44321b580d9a7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582274"
---
# <a name="mbr2gpt-tool-test-guidance"></a>MBR2GPT ツール テスト ガイダンス


**MBR2GPT.EXE** は、ディスク上のデータを変更または削除せずに、ディスクをマスター ブート レコード (MBR) から GUID パーティション テーブル (GPT) パーティション スタイルに変換します。 ツールは、Windows プレインストール環境 (Windows PE) のコマンド プロンプトから実行するのには設計されていますが、完全な Windows 10 オペレーティング システム (OS) から実行することもできます。

ツールの詳細については、使用状況に関する情報を含むとトラブルシューティングのガイダンス、ドキュメント参照してください、Technet の記事の[MBR2GPT](https://docs.microsoft.com/windows/deployment/mbr-to-gpt)します。

## <a name="sample-checklist-when-verifying-conversion-from-biosmbr-to-uefigpt"></a>BIOS MBR/から UEFI/GPT への変換を確認するときのサンプル チェックリスト

- MBR2GPT を実行する前に
    - コンピューターが BIOS モードで起動した現在を確認する msinfo32 を実行します。
    - Windows 64 ビット OS がインストールされていることを確認する msinfo32 を実行します。
    - システム ディスクでは、最大で 3 つのプライマリ パーティションを MBR に、パーティションの少なくとも 1 つはアクティブとしてマークされていること。
    - デバイスのファームウェアでは、ファームウェアのメニューで関連する設定を探すことによって、または PC/ファームウェアの製造元に確認して、UEFI ブートがサポートされていることを確認します。
- MBR2GPT を実行した後が UEFI モードで Windows 10 に起動する前に
    - ファームウェアのメニューで、ブート モードの設定が、「UEFI のみ」(または同等) に設定されていることを確認します。
    - ファームウェアのメニューで互換性サポート モジュール (CSM) が無効になっていることを確認セキュア ブートが有効になっています。
- Windows 10 UEFI モードで起動した後
    - デバイスが UEFI モードで起動したことを確認する msinfo32 を実行し、セキュア ブートが有効になっています。
    - 基幹業務 (LOB) アプリケーションが正しく機能してもいることを確認します。

**注**システム ファームウェアとデバイスの製造元によって異なることができます。 質問や懸念事項がある場合について、デバイスの製造元に問い合わせてください。

## <a name="test-scenarios"></a>テスト シナリオ

### <a name="conversion-after-an-in-place-upgrade"></a>インプレース アップグレード後の変換

1.  BIOS モードで Windows 7、8、または 8.1 を実行するデバイスを起動します。

2.  デバイスは、Windows 10、バージョン 1507、バージョン 1511、1607 BIOS モードでのバージョンにアップグレードします。

3.  Windows pe、バージョン 1703 では、Windows Assessment and Deployment Kit for Windows 10 バージョン 1703 から取得できるデバイスを起動します。

4.  MBR2GPT を実行します。Windows 10 がインストールされているディスクに対して実行可能ファイルです。

5.  UEFI モードで起動、セキュア ブートを有効にする、および、CSM を無効にするファームウェアを再構成するには。

    - ファームウェアのメニューで、関連する設定を変更します。

    または

    - PC またはファームウェアの製造元によって提供されるツールを実行します。

6.  UEFI モードで Windows 10 の起動します。

### <a name="conversion-as-part-of-re-imaging"></a>再イメージ化の一部として変換

1.  BIOS モードで Windows 7、8、または 8.1 を実行するデバイスを起動します。

2.  データと USMT のスキャン状態を使用して設定をキャプチャします。

3.  Windows pe、バージョン 1703 では、Windows Assessment and Deployment Kit for Windows 10 バージョン 1703 から取得できるデバイスを起動します。

4.  Windows 10、バージョン 1703 イメージをデプロイします。

5.  MBR2GPT を実行します。Windows 10 がインストールされているディスクに対して実行可能ファイルです。

6.  UEFI モードで起動、セキュア ブートを有効にする、および、CSM を無効にするファームウェアを再構成するには。

    - ファームウェアのメニューで、関連する設定を変更します。

    または

    - PC またはファームウェアの製造元によって提供されるツールを実行します。

7.  UEFI モードで Windows 10 の起動します。

データと USMT の負荷の状態を使用して設定を復元します。

### <a name="conversion-as-part-of-hyper-v-generation-1-vm"></a>HYPER-V 第 1 世代の VM

1.  BIOS モードで Windows 7、8、または 8.1 を実行するデバイスを起動します。

2.  VM は、Windows 10 バージョン 1507、バージョン 1511、1607 BIOS モードでのバージョンにアップグレードします。

3.  Windows pe、バージョン 1703 では、Windows Assessment and Deployment Kit for Windows 10 バージョン 1703 から取得できる VM を起動します。

4.  変換を実行するディスクの数と照らし合わせて MBR2GPT.exe を実行します。

5.  VHD を切断します。

6.  UEFI で 2 つの VM をサポートし、上記の手順 5 から作成された上記の VHD をアタッチの生成を作成します。

7.  Windows 10 バージョン 1703 を汎用を使用して、UEFI モードでの 2 つの VM を起動します。

**注**保護が中断されている限り、上記のシナリオのいずれかの MBR ディスクでは、BitLocker で暗号化されたボリュームを変換することができます。 変換後に BitLocker を再開するには、既存の保護機能を削除して再作成する必要があります。

## <a name="troubleshooting"></a>トラブルシューティング

MBR2GPT を参照してください。EXE[トラブルシューティング](https://docs.microsoft.com/windows/deployment/mbr-to-gpt#troubleshooting)ログ ファイルの場所と追加のヘルプについてはドキュメントです。 スクリプトまたは SCCM/MDT タスク シーケンスを使用してこのツールの使用を自動化している場合、返されたコードのドキュメントに記載されているハンドラーのスクリプトを作成することができます。

## <a name="related-resources"></a>関連リソース

[MBR2GPT.EXE](https://docs.microsoft.com/windows/deployment/mbr-to-gpt)



