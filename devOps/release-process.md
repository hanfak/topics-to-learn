## Going to Production

- Check for go ahead
- deploy
- check status page
  - No errors in status page
  - status page has correct version
- Check database if necessary
  - Check migrations done
  - Check data has changed or tables etc changed
- Check kubernetes to see new apps deployed
- Update release notes
- Check logs (ie splunk or on container)
- run a smoke test
  - ie to check certificates

## Environments

- Test
- Performance
- Stage
- Production
