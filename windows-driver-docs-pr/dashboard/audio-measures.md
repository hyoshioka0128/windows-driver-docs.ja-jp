---
title: オーディオの測定値
description: オーディオの測定値の定義
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 50956d9fda24b7d055a687b633deba14b9b22b9e
ms.sourcegitcommit: 9f6f7d9e327ac3bd34643d8b062e11958a0fe05f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2019
ms.locfileid: "71195761"
---
# <a name="audio-measures"></a>オーディオの測定値

## <a name="audio-stream-initialization"></a>オーディオ ストリームの初期化

アプリケーション (または Windows コンポーネント) でオーディオを再生または録音するときは、さまざまなオーディオ API のいずれかが使用されます。

すべてのオーディオ API では、最終的にコア オーディオ API 呼び出し [IAudioClient::Initialize](https://docs.microsoft.com/en-us/windows/win32/api/audioclient/nf-audioclient-iaudioclient-initialize) を呼び出します。 これにより、アプリケーションと Windows オーディオ エンジン間の接続と、Windows オーディオ エンジンとオーディオ ドライバー間の接続が作成されます。

IAudioClient:: Initialize の呼び出しが失敗した場合、一部の例外を除いて、アプリケーションはオーディオを使用できません。 IAudioClient:: Initialize エラーの中には、特に問題なく、無視されるものもあります。これらのエラーの一覧については[付録](measure-appendix.md)に記載されています。

呼び出しの結果は、**Microsoft.Windows.Audio.Client** プロバイダーの **AudioClientInitialize** テレメトリ イベントのログに記録されています。 呼び出しが成功した場合、**HResult** フィールドは 0 になり、呼び出しが失敗した場合は負の数値になります。

次のオーディオの測定値は、IAudioClient:: Initialize の成功を追跡します。
* [少なくとも 1 つのオーディオ ストリーム初期化エラーが発生したマシンの割合](pct-machines-with-at-least-one-audio-stream-initialization-failure.md)
* [subpar ストリーム初期化成功率のあるマシンの割合](pct-machines-with-subpar-stream-initialization-success-rate.md)

## <a name="audio-user-mode-reliability"></a>オーディオ ユーザーモードの信頼性

カーネル ストリーミングのオーディオ ドライバーはカーネル モードで実行されます。 オーディオ ドライバーが例外にヒットすると、ブルー スクリーン (BSOD) またはグリーン スクリーン (GSOD) が発生します。

オーディオ カーネルモードの信頼性の問題に特化する対策はありませんが、カーネルモードの信頼性の問題に対する一般的な対策はあります。

Windows 共有モード オーディオ エンジンは、ユーザー モードで実行されます。 特に、"Windows オーディオ" サービスの AudioSrv.dll (AudioSrv) は専用の svchost.exe プロセスで実行されます。 また、ヘルパーである "Windows オーディオ デバイス グラフ アイソレーション" プロセスの audiodg.exe (AudioDg) も起動します。

オーディオ IHV には、オーディオ処理オブジェクト (APO) というユーザーモードのオーディオ エンジンへのプラグインを含めることができます。

APO で例外が発生した場合、ブルー スクリーンは発生しませんが、Windows オーディオ エンジンはクラッシュします。 アプリケーションからの呼び出しが短時間で完了していることを確認するウォッチドッグ タイマーもあります。 呼び出しがスタックした場合、ウォッチドッグはそれを感知し、Windows オーディオ エンジンを強制的にクラッシュさせます。

いずれにしても、オーディオ エンジンを再起動できるようになるまで、システム上のすべてのオーディオは失われます。

AudioDg がクラッシュし、AudioSrv が感知すると、**Microsoft.Windows.Audio.Service** プロバイダーから **AudioDgCrash** テレメトリ イベントがログに記録されます。 (以前のバージョンの Windows 10 では、イベントは **AudioDg-Crash** でした。)

AudioSrv がクラッシュし、AudioDg が感知すると、**Microsoft.Windows.Audio.DeviceGraph** プロバイダーから **AudioSrvSvchostCrash** テレメトリ イベントがログに記録されます。 (以前のバージョンの Windows 10 では、イベントは **AudioDg-Crash** でした。)

オーディオ サービスが停止した場合、**Microsoft.Windows.Audio.Service** プロバイダーから **Hang** テレメトリ イベントがログに記録されます。 (以前の一部のバージョンの Windows 10 では、特定の種類の停止の場合、**Microsoft.Windows.Audio.DeviceGraph** プロバイダーから **Hang** イベントもログに記録されていました。)

次のオーディオの測定値は、Windows オーディオ エンジンの信頼性を追跡します。
* [少なくとも 1 つのオーディオ クラッシュが発生したマシンの割合](percent-machines-with-at-least-one-audio-crash.md)
* [少なくとも 1 つのオーディオ ハングが発生したマシンの割合](pct-machines-with-at-least-one-audio-hang.md)
