---
title: MBR2GPT ツール テスト ガイダンス
description: MBR2GPT ツール テスト ガイダンス
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 62c68c1baba40467530339ffdcdd96ff4111163e
ms.sourcegitcommit: 9b764ce48a3af451528a4229cdfb62221ef56942
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75607678"
---
# <a name="mbr2gpt-tool-test-guidance"></a>MBR2GPT ツール テスト ガイダンス

**MBR2GPT.EXE** は、ディスク上のデータを変更または削除せずに、ディスクをマスター ブート レコード (MBR) から GUID パーティション テーブル (GPT) パーティション スタイルに変換します。 このツールは、Windows プレインストール環境 (Windows PE) コマンドプロンプトから実行するように設計されていますが、完全な Windows 10 オペレーティングシステム (OS) から実行することもできます。

使用方法の詳細とトラブルシューティングのガイダンスについては、 [mbr2gpt.exe](https://docs.microsoft.com/windows/deployment/mbr-to-gpt)のドキュメントを参照してください。

## <a name="sample-checklist-when-verifying-conversion-from-biosmbr-to-uefigpt"></a>BIOS/MBR から UEFI/GPT への変換を確認する場合のサンプルチェックリスト

- MBR2GPT.EXE を実行する前
  - コンピューターが BIOS モードで現在ブートされていることを確認するには、msinfo32 を実行します。
  - Windows 64 ビット OS がインストールされていることを確認するには、msinfo32 を実行します
  - システムディスクに MBR に最大3個のプライマリパーティションがあり、少なくとも1つのパーティションがアクティブとしてマークされていることを確認します。
  - [ファームウェア] メニューで関連する設定を探すか、または PC/ファームウェアの製造元に確認して、デバイスのファームウェアが UEFI ブートをサポートしていることを確認します。
- MBR2GPT.EXE を実行した後、UEFI モードで Windows 10 を起動する前
  - [ファームウェア] メニューで、[ブートモード] の設定が "UEFI のみ" (またはそれと同等) に設定されていることを確認します。
  - [ファームウェア] メニューで、互換性サポートモジュール (CSM) が無効になっており、セキュアブートが有効になっていることを確認します。
- UEFI モードで Windows 10 を起動した後
  - [Msinfo32] を実行して、デバイスが UEFI モードで起動され、セキュアブートが有効になっていることを確認します。
  - 基幹業務 (LOB) アプリケーションが正常に機能していることを確認する

> [!NOTE]
> システムファームウェアは、製造元とデバイスによって異なる場合があります。 不明な点や懸念事項がある場合は、デバイスの製造元に問い合わせてください。

## <a name="test-scenarios"></a>テスト シナリオ

### <a name="conversion-after-an-in-place-upgrade"></a>インプレースアップグレード後の変換

1. Windows 7、8、または8.1 を実行しているデバイスを BIOS モードで起動します。

1. BIOS モードで、デバイスを Windows 10 バージョン1507、バージョン1511、またはバージョン1607にアップグレードします。

1. Windows PE バージョン1703でデバイスを起動します。このバージョンは、windows 10 バージョン1703の Windows アセスメント & amp; デプロイメントキットから入手できます。

1. MBR2GPT.EXE を実行します。Windows 10 がインストールされているディスクに対する EXE。

1. UEFI モードで起動するようにファームウェアを再構成し、セキュアブートを有効にし、CSM を無効にします。

    - [ファームウェア] メニューの関連する設定の変更

    または

    - PC またはファームウェアの製造元が提供するツールの実行

1. UEFI モードで Windows 10 を起動する

### <a name="conversion-as-part-of-re-imaging"></a>再イメージングの一部としての変換

1. Windows 7、8、または8.1 を実行しているデバイスを BIOS モードで起動します。

1. USMT のスキャン状態を使用してデータと設定をキャプチャします。

1. Windows PE バージョン1703でデバイスを起動します。このバージョンは、windows 10 バージョン1703の Windows アセスメント & amp; デプロイメントキットから入手できます。

1. Windows 10 バージョン1703イメージを展開します。

1. MBR2GPT.EXE を実行します。Windows 10 がインストールされているディスクに対する EXE。

1. UEFI モードで起動するようにファームウェアを再構成し、セキュアブートを有効にし、CSM を無効にします。

    - [ファームウェア] メニューの関連する設定の変更

    または

    - PC またはファームウェアの製造元が提供するツールの実行

1. UEFI モードで Windows 10 を起動する

USMT の読み込み状態を使用して、データと設定を復元します。

### <a name="conversion-as-part-of-hyper-v-generation-1-vm"></a>Hyper-v 第1世代 VM の一部としての変換

1. Windows 7、8、または8.1 を実行しているデバイスを BIOS モードで起動します。

1. BIOS モードで、VM を Windows 10 バージョン1507、バージョン1511、またはバージョン1607にアップグレードします。

1. Windows PE バージョン1703で VM を起動します。このバージョンは、windows 10 バージョン1703の Windows アセスメント & amp; デプロイメントキットから入手できます。

1. 変換を実行するディスク番号に対して MBR2GPT.EXE を実行します。

1. VHD の切断

1. UEFI サポートを使用して第2世代の VM を作成し、上記の手順5で作成した VHD をアタッチします。

1. Gen 2 VM を使用して、UEFI モードで Windows 10 バージョン1703を起動します。

> [!NOTE]
> 上記のいずれかのシナリオでは、保護が中断されている間は、BitLocker で暗号化されたボリュームを使用して MBR ディスクを変換できます。 変換後に BitLocker を再開するには、既存の保護機能を削除して再作成する必要があります。

## <a name="troubleshooting"></a>[トラブルシューティング]

MBR2GPT.EXE を参照してください。EXE の[トラブルシューティング](https://docs.microsoft.com/windows/deployment/mbr-to-gpt#troubleshooting)に関するドキュメントでは、ログファイルの場所とその他のヘルプについて説明します。 このツールの使用をスクリプトまたは Microsoft Endpoint Configuration Manager/Microsoft Deployment Toolkit (MDT) のタスクシーケンスによって自動化する場合は、ドキュメントで説明されている、返されるコードのハンドラーをスクリプト化できます。

## <a name="related-resources"></a>関連リソース

[MBR2GPT.EXE.EXCEL.EXE](https://docs.microsoft.com/windows/deployment/mbr-to-gpt)
