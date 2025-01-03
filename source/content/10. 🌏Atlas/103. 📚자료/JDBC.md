JDBC를 활용한 대용량 데이터 저장

```java
@Repository
public class ProcessLevelJpaStore implements ProcessLevelStore {
	private final JdbcTemplate jdbcTemplate;

	public ProcessLevelJpaStore(JdbcTemplate jdbcTemplate) {
		this.jdbcTemplate = jdbcTemplate;
	}

	@Override
	public void bulkSave(List<ProcessLevel> processLevelList) {
		batchInsert(1000, processLevelList);
	}

	private void batchInsert(int batchSize, List<ProcessLevel> processLevelList) {
		jdbcTemplate.batchUpdate(
			"INSERT INTO PROCESS_LEVEL (" +
			"SEQ, CD_TP" +
			") VALUES (" +
			"?, ?" +
			")",
			new BatchPreparedStatementSetter() {
				@Override
				public void setValues(PreparedStatement ps, int i) throws SQLException {
					ProcessLevel processLevel = processLevelList.get(i);
					ps.setBigDecimal(1, processLevel.getSeq());
					ps.setString(2, processLevel.getCdTp());
				}

				@Override
				public int getBatchSize() {
					return processLevelList.size();
				}
			});
	}
}
```