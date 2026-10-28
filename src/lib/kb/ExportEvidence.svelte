<script lang="ts">
  import reports from '#lib/data/reports-4471.json';
  import { uniqueById, type Report } from '#lib/kb/causes';

  const unique = uniqueById(reports as Report[]);
  const merged = unique.filter((r) => r.mergedInto === 4471);
  const tags = Object.entries(merged.reduce<Record<string, number>>((counts, r) => {
    counts[r.meta.intakeTag] = (counts[r.meta.intakeTag] ?? 0) + 1;
    return counts;
  }, {})).map(([tag, count]) => `${tag} ×${count}`).join(' · ');
</script>

<p>
  The export contains <strong>{reports.length}</strong> rows and <strong>{unique.length}</strong>
  unique report IDs: <strong>{reports.length - unique.length}</strong> overlapping rows are not
  additional reports. <strong>{merged.length}</strong> unique reports are merged into #4471.
  The table below classifies them by tenant locale, booking form and entry channel.
</p>
<p>
  Counting intake tags alone would give <code>{tags}</code>. Those are not cause counts.
</p>
