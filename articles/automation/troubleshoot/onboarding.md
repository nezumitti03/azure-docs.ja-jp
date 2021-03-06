---
title: Azure Automation 管理ソリューションのオンボードに関するトラブルシューティング
description: Azure Automation ソリューションのオンボード エラーをトラブルシューティングする方法について説明します。
services: automation
author: mgoedtel
ms.author: magoedte
ms.date: 05/22/2019
ms.topic: conceptual
ms.service: automation
manager: carmonm
ms.openlocfilehash: 371094ecba5168fd32a7af9fb81a71eb722efc91
ms.sourcegitcommit: 11572a869ef8dbec8e7c721bc7744e2859b79962
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/05/2020
ms.locfileid: "82836531"
---
# <a name="troubleshoot-solution-onboarding"></a>ソリューションのオンボードに関するトラブルシューティング

Azure Automation Update Management ソリューションをオンボードするとき、または Change Tracking および Inventory ソリューションをオンボードするとき、エラー メッセージが表示される場合があります。 この記事では、発生する可能性があるさまざまなエラーと、その解決方法について説明します。

## <a name="known-issues"></a>既知の問題

### <a name="scenario-renaming-a-registered-node-requires-unregister-or-register-again"></a><a name="node-rename"></a>シナリオ:登録されたノードの名前を変更するには、登録の解除または再登録が必要です

#### <a name="issue"></a>問題

ノードが Azure Automation に登録された後、オペレーティング システムのコンピューター名が変更されました。 そのノードからのレポートは、引き続き元の名前で表示されます。

#### <a name="cause"></a>原因

登録されたノードの名前を変更しても、Azure Automation 内のノード名は更新されません。

#### <a name="resolution"></a>解決策

Azure Automation State Configuration からノードの登録を解除し、再度登録してください。 それより前にサービスに発行されたレポートは、使用できなくなります。

### <a name="scenario-re-signing-certificates-via-https-proxy-isnt-supported"></a><a name="resigning-cert"></a>シナリオ:HTTPS プロキシ経由の証明書の再署名がサポートされていません

#### <a name="issue"></a>問題

HTTPS トラフィックを終了してから新しい証明書を使用してそのトラフィックを再暗号化するプロキシ ソリューションを介して接続する場合に、その接続がサービスによって許可されません。

#### <a name="cause"></a>原因

Azure Automation では、トラフィックの暗号化に使用される証明書の再署名はサポートされていません。

#### <a name="resolution"></a>解決策

現時点では、この問題の回避策はありません。

## <a name="general-errors"></a>一般エラー

### <a name="scenario-onboarding-fails-with-the-message-the-solution-cannot-be-enabled"></a><a name="missing-write-permissions"></a>シナリオ:オンボードが失敗し、"ソリューションを有効にできません" というメッセージが表示されます

#### <a name="issue"></a>問題

VM をソリューションにオンボードしようとすると、次のメッセージのいずれかが表示されます。

```error
The solution cannot be enabled due to missing permissions for the virtual machine or deployments
```

```error
The solution cannot be enabled on this VM because the permission to read the workspace is missing
```

#### <a name="cause"></a>原因

このエラーは、VM またはワークスペースに対するアクセス許可、またはユーザーのアクセス許可が正しくないか、不足しているために発生します。

#### <a name="resolution"></a>解決策

[マシンをオンボードするために必要な正しいアクセス許可](../automation-role-based-access-control.md#onboarding-permissions)があることを確認してから、再度ソリューションをオンボードしてみてください。 `The solution cannot be enabled on this VM because the permission to read the workspace is missing` というエラー メッセージが発生する場合は、ワークスペースに VM がオンボードされているかどうかを調べることができる `Microsoft.OperationalInsights/workspaces/read` アクセス許可があることを確認してください。

### <a name="scenario-onboarding-fails-with-the-message-failed-to-configure-automation-account-for-diagnostic-logging"></a><a name="diagnostic-logging"></a>シナリオ:オンボードが失敗し、"診断ログのオートメーション アカウントを構成できませんでした" というメッセージが表示されます

#### <a name="issue"></a>問題

VM をソリューションにオンボードしようとすると、次のメッセージが表示されます。

```error
Failed to configure automation account for diagnostic logging
```

#### <a name="cause"></a>原因

このエラーは、価格レベルがサブスクリプションの課金モデルと一致しない場合に発生することがあります。 詳細については、「[Azure Monitor での使用量と推定コストの監視](https://aka.ms/PricingTierWarning)」を参照してください。

#### <a name="resolution"></a>解決策

Log Analytics ワークスペースを手動で作成し、オンボード プロセスを繰り返して、作成したワークスペースを選択します。

### <a name="scenario-computergroupqueryformaterror"></a><a name="computer-group-query-format-error"></a>シナリオ:ComputerGroupQueryFormatError

#### <a name="issue"></a>問題

このエラー コードは、ソリューションを選択するために使用された、コンピューター グループを検索する保存済みクエリの形式が正しくないことを意味します。 

#### <a name="cause"></a>原因

クエリが変更されたか、システムによってそれが変更されたことが考えられます。

#### <a name="resolution"></a>解決策

そのソリューションに対するクエリを削除してから、ソリューションを再度オンボードすれば、クエリが再度作成されます。 クエリはワークスペース内の、 **[保存された検索条件]** にあります。 クエリの名前は **MicrosoftDefaultComputerGroup** です。クエリのカテゴリは、関連付けられたソリューションの名前となります。 複数のソリューションが有効な場合は、**MicrosoftDefaultComputerGroup** クエリが複数回 **[保存された検索条件]** に表示されます。

### <a name="scenario-policyviolation"></a><a name="policy-violation"></a>シナリオ:PolicyViolation

#### <a name="issue"></a>問題

このエラー コードは、1 つ以上のポリシーの違反が原因でデプロイが失敗したことを示します。

#### <a name="cause"></a>原因 

ポリシーによって操作の完了が阻止されています。

#### <a name="resolution"></a>解決策

ソリューションを正常にデプロイするには、指定されたポリシーの変更を検討する必要があります。 定義可能なポリシーが多数あるため、必要になる変更は、違反しているポリシーによって異なります。 たとえば、リソース グループに対して、含まれている一部のリソースの内容を変更するためのアクセス許可を拒否するポリシーが定義されている場合は、次のいずれかの修正を選択できます。

* ポリシーを完全に削除する
* 別のリソース グループへのソリューションのオンボードを試す。
* Automation アカウントなどの特定のリソースに対してポリシーを再ターゲットする。
* 拒否するようにポリシーが構成されているリソースのセットを変更する。

Azure portal の右上にある通知を確認するか、Automation アカウントを含むリソース グループに移動し、 **[設定]** の **[デプロイ]** を選択して、失敗したデプロイを表示します。 Azure Policy の詳細については、[Azure Policy の概要](../../governance/policy/overview.md?toc=%2fazure%2fautomation%2ftoc.json)に関するページを参照してください。

### <a name="scenario-errors-trying-to-unlink-a-workspace"></a><a name="unlink"></a>シナリオ:ワークスペースのリンクを解除しようとすると発生するエラー

#### <a name="issue"></a>問題

ワークスペースのリンクを解除しようとすると、次のエラー メッセージが届きます。

```error
The link cannot be updated or deleted because it is linked to Update Management and/or ChangeTracking Solutions.
```

#### <a name="cause"></a>原因

このエラーは、Log Analytics ワークス ペース内に Automation アカウントに依存するアクティブなソリューションがまだ存在し、Log Analytics ワークスペースがリンクされている場合に発生します。

### <a name="resolution"></a>解決策

次のソリューションを使用している場合は、ご利用のワークスペースから削除する必要があります。

* 更新管理
* 変更履歴とインベントリ
* 勤務時間外に VM を起動/停止する

ソリューションを削除すると、ワークスペースのリンクを解除できます。 ご利用のワークスペースおよび Automation アカウントから、これらのソリューションの既存の成果物をクリーンアップすることが重要です。

* Update Management の場合は、Automation アカウントから、**更新プログラムのデプロイ (スケジュール)** を削除します。
* Start/Stop VMs during off-hours の場合、 **[設定]**  >  **[ロック]** で、Automation アカウントのソリューション コンポーネントに対するロックを解除します。 詳細については、[Start/Stop VMs during off-hours ソリューションの削除](../automation-solution-vm-management.md#remove-the-solution)に関するページを参照してください。

## <a name="log-analytics-for-windows-extension-failures"></a><a name="mma-extension-failures"></a>Windows 拡張機能用の Log Analytics のエラー

[!INCLUDE [log-analytics-agent-note](../../../includes/log-analytics-agent-note.md)] 

Windows 拡張機能用の Log Analytics エージェントのインストールは、さまざまな理由で失敗する可能性があります。 次のセクションでは、Windows 拡張機能用の Log Analytics エージェントのデプロイ中にエラーを引き起こす可能性があるオンボードに関する問題について説明します。

>[!NOTE]
>Windows 用 Log Analytics エージェントは、Microsoft Monitoring Agent (MMA) の Azure Automation で現在使用されている名前です。

### <a name="scenario-an-exception-occurred-during-a-webclient-request"></a><a name="webclient-exception"></a>シナリオ:WebClient 要求で例外が発生した

VM 上の Windows 拡張機能用の Log Analytics が外部リソースと通信できず、デプロイが失敗します。

#### <a name="issue"></a>問題

返されるエラー メッセージの例を次に示します。

```error
Please verify the VM has a running VM agent, and can establish outbound connections to Azure storage.
```

```error
'Manifest download error from https://<endpoint>/<endpointId>/Microsoft.EnterpriseCloud.Monitoring_MicrosoftMonitoringAgent_australiaeast_manifest.xml. Error: UnknownError. An exception occurred during a WebClient request.
```

#### <a name="cause"></a>原因

このエラーの原因として考えられるものは次のとおりです。

* VM 内で構成されているプロキシでは、特定のポートのみ許可されます。
* ファイアウォールの設定によって、必要なポートとアドレスへのアクセスがブロックされた。

#### <a name="resolution"></a>解決策

適切なポートとアドレスが通信のために開いていることを確認します。 ポートとアドレスの一覧は、[ネットワークの計画](../automation-hybrid-runbook-worker.md#network-planning)に関する記事を参照してください。

### <a name="scenario-install-failed-because-of-transient-environment-issues"></a><a name="transient-environment-issue"></a>シナリオ:環境の一時的な問題のためにインストールが失敗した

Windows 拡張機能用の Log Analytics のインストールは、デプロイ時に別のインストールまたは操作によって妨げられるため、失敗しました。

#### <a name="issue"></a>問題

返されるエラー メッセージの例を次に示します。

```error
The Microsoft Monitoring Agent failed to install on this machine. Please try to uninstall and reinstall the extension. If the issue persists, please contact support.
```

```error
'Install failed for plugin (name: Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent, version 1.0.11081.4) with exception Command C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\1.0.11081.4\MMAExtensionInstall.exe of Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent has exited with Exit code: 1618'
```

```error
'Install failed for plugin (name: Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent, version 1.0.11081.2) with exception Command C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\1.0.11081.2\MMAExtensionInstall.exe of Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent has exited with Exit code: 1601'
```

#### <a name="cause"></a>原因

このエラーの原因として考えられるものは次のとおりです。

* 別のインストールが進行中です。
* テンプレートのデプロイ中にシステムの再起動がトリガーされます。

#### <a name="resolution"></a>解決策

このエラーは本質的に一時的なものです。 デプロイを再試行して拡張機能をインストールしてください。

### <a name="scenario-installation-timeout"></a><a name="installation-timeout"></a>シナリオ:インストールのタイムアウト

Windows 拡張機能用の Log Analytics のインストールがタイムアウトのために完了しませんでした。

#### <a name="issue"></a>問題

返される可能性のあるエラー メッセージの例を次に示します。

```error
Install failed for plugin (name: Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent, version 1.0.11081.4) with exception Command C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\1.0.11081.4\MMAExtensionInstall.exe of Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent has exited with Exit code: 15614
```

#### <a name="cause"></a>原因

この種のエラーは、インストール中に VM の負荷が大きくなったために発生します。

### <a name="resolution"></a>解決策

VM の負荷が小さい場合に、Windows 拡張機能用の Log Analytics エージェントをインストールしてみてください。

## <a name="next-steps"></a>次のステップ

該当する問題がここにない場合、または問題を解決できない場合は、追加のサポートを受けるために、次のいずれかのチャネルをお試しください。

* [Azure フォーラム](https://azure.microsoft.com/support/forums/)を通じて Azure エキスパートから回答を得ることができます。
* [@AzureSupport](https://twitter.com/azuresupport) (カスタマー エクスペリエンスを向上させるための Microsoft Azure の公式アカウント) に連絡する。 Azure サポートにより、Azure コミュニティの回答、サポート、エキスパートと結び付けられます。
* Azure サポート インシデントを送信する。 [Azure サポートのサイト](https://azure.microsoft.com/support/options/)に移動して、 **[サポートを受ける]** を選択します。
