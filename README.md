# Ansible Role: Kibana

This role can install Kibana and connect to elasticsearch in different configuration:
- Elasticsearch standalone server
- Elasticsearch cluster

Also with various configuration:
- SSL encryption

## Requirements

- Elasticsearch server or cluster ready to connect
- If you're install with Elaticsearch cluster role. The kibana node also need to install with Elasticsearch client node configuration and point url to `http://localhost:9200`

## Role Variables

- `kibana_log_path`: Specified log path (No data path since there's no persistence data that need to keep)
- `kibana_server_port`: Specified server port
- `kibana_ssl_enabled`: Enable/disable SSL for kibana
- `kibana_host_ssl_key_file_path`: SSL private key on your host
- `kibana_host_ssl_cert_file_path`: SSL certificate on your host
- `kibana_host_ssl_ca_file_path`: SSL CA on your host (optional)
- `kibana_elasticsearch_url`: Specified which elasticsearch URL to connect. Default at `http://localhost:9200`
- `kibana_password`: Specified password for built-in `kibana` user on Elasticsearch server/cluster

## Dependencies

- https://github.com/opsta/ansible-java

## Example Inventory

- Standalone and connect to another standalone Elasticsearch server
```ini
[kibana]
kibana ansible_user=ubuntu ansible_host=x.x.x.x ansible_port=22
```

- Standalone and connect to Elasticsearch cluster
- Multiple roles cluster
```ini
elasticsearch-master-1 ansible_user=ubuntu ansible_host=x.x.x.x ansible_port=22
elasticsearch-master-2 ansible_user=ubuntu ansible_host=x.x.x.x ansible_port=22
elasticsearch-master-3 ansible_user=ubuntu ansible_host=x.x.x.x ansible_port=22
elasticsearch-data-1 ansible_user=ubuntu ansible_host=x.x.x.x ansible_port=22
elasticsearch-data-2 ansible_user=ubuntu ansible_host=x.x.x.x ansible_port=22
kibana ansible_user=ubuntu ansible_host=x.x.x.x ansible_port=22

[elasticsearch-master]
elasticsearch-master-1
elasticsearch-master-2
elasticsearch-master-3

[elasticsearch-data]
elasticsearch-data-1
elasticsearch-data-2

[elasticsearch-client]
kibana

[kibana]
kibana
```

## Example Playbook

```yaml
    - hosts: all
      roles:
        - ansible-kibana
```

## License

MIT

## Author Information

Opsta (Thailand) Co.,Ltd.

