import React, { useState } from 'react';
import { 
  StyleSheet, 
  Text, 
  View, 
  Image, 
  TextInput, 
  Pressable, 
  ScrollView, 
  SafeAreaView, 
  StatusBar 
} from 'react-native';

export default function App() {
  const [constellation, setConstellation] = useState('');
  const [notes, setNotes] = useState('');
  const [entries, setEntries] = useState([
    { id: '1', title: 'Órion brilhante', date: '05/09/2026', desc: 'Noite limpa, vi as Três Marias perfeitamente.' }
  ]);

  const handleAddEntry = () => {
    if (constellation.trim() === '') return;
    const newEntry = {
      id: Date.now().toString(),
      title: constellation,
      date: 'Hoje',
      desc: notes || 'Nenhuma observação extra.'
    };
    setEntries([newEntry, ...entries]);
    setConstellation('');
    setNotes('');
  };

  return (
    <SafeAreaView style={styles.safeArea}>
      <StatusBar barStyle="light-content" backgroundColor="#2D1248" />
      
      {/* Cabeçalho */}
      <View style={styles.header}>
        <Text style={styles.headerTitle}>✨ Diário Estelar</Text>
        <Text style={styles.headerSubtitle}>Guarde os segredos do seu céu</Text>
      </View>

      {/* Conteúdo Principal com ScrollView */}
      <ScrollView contentContainerStyle={styles.scrollContainer}>
        
        {/* Seção de Cadastro Rápido */}
        <View style={styles.card}>
          <Text style={styles.cardTitle}>Registrar Nova Observação</Text>
          
          <TextInput 
            style={styles.input}
            placeholder="Nome da estrela ou constelação"
            placeholderTextColor="#C9A8E8"
            value={constellation}
            onChangeText={setConstellation}
          />

          <TextInput 
            style={[styles.input, styles.textArea]}
            placeholder="Como estava o céu? O que você sentiu?"
            placeholderTextColor="#C9A8E8"
            multiline
            value={notes}
            onChangeText={setNotes}
          />

          <Pressable style={styles.button} onPress={handleAddEntry}>
            <Text style={styles.buttonText}>Salvar no Firmamento</Text>
          </Pressable>
        </View>

        {/* Banner Ilustrativo */}
        <View style={styles.bannerContainer}>
          <Image 
            source={{ uri: 'https://images.unsplash.com/photo-1506703719100-a0f3a48c0f86?q=80&w=600&auto=format&fit=crop' }} 
            style={styles.bannerImage}
          />
          <Text style={styles.bannerText}>"Olhe para as estrelas e não para os seus pés."</Text>
        </View>

        {/* Lista de Registros Anteriores */}
        <View style={styles.sectionContainer}>
          <Text style={styles.sectionTitle}>Seus Registros Recentes</Text>
          
          {entries.map((item) => (
            <View key={item.id} style={styles.entryCard}>
              <View style={styles.entryHeader}>
                <Text style={styles.entryTitle}>🌟 {item.title}</Text>
                <Text style={styles.entryDate}>{item.date}</Text>
              </View>
              <Text style={styles.entryDesc}>{item.desc}</Text>
            </View>
          ))}
        </View>

      </ScrollView>

      {/* Rodapé Fixo */}
      <View style={styles.footer}>
        <Text style={styles.footerText}>Explorador Noturno • Versão 1.0</Text>
      </View>

    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  safeArea: {
    flex: 1,
    backgroundColor: '#2D1248', // Roxo profundo de fundo
  },
  header: {
    paddingVertical: 16,
    paddingHorizontal: 20,
    backgroundColor: '#431C6B', // Roxo intermediário vibrante
    borderBottomWidth: 1,
    borderBottomColor: '#6A2C91',
    alignItems: 'center',
  },
  headerTitle: {
    fontSize: 22,
    fontWeight: 'bold',
    color: '#E8D7F1', // Lilás bem clarinho (quase branco)
  },
  headerSubtitle: {
    fontSize: 12,
    color: '#C9A8E8', // Lilás suave
    marginTop: 2,
  },
  scrollContainer: {
    padding: 16,
    paddingBottom: 30,
  },
  card: {
    backgroundColor: '#431C6B',
    borderRadius: 12,
    padding: 16,
    marginBottom: 20,
    shadowColor: '#BA68C8',
    shadowOpacity: 0.3,
    shadowRadius: 6,
    elevation: 4,
    borderWidth: 1,
    borderColor: '#6A2C91',
  },
  cardTitle: {
    fontSize: 16,
    fontWeight: '600',
    color: '#E8D7F1',
    marginBottom: 12,
  },
  input: {
    backgroundColor: '#351657', // Roxo escuro para dar contraste nos inputs
    borderWidth: 1,
    borderColor: '#7B34A4',
    borderRadius: 8,
    paddingHorizontal: 12,
    paddingVertical: 10,
    color: '#FFFFFF',
    fontSize: 14,
    marginBottom: 12,
  },
  textArea: {
    height: 70,
    textAlignVertical: 'top',
  },
  button: {
    backgroundColor: '#BA68C8', // Lilás/Roxo claro bem destacado para o botão
    borderRadius: 8,
    paddingVertical: 12,
    alignItems: 'center',
  },
  buttonText: {
    color: '#2D1248', // Texto escuro para contraste perfeito no botão claro
    fontWeight: 'bold',
    fontSize: 14,
  },
  bannerContainer: {
    borderRadius: 12,
    overflow: 'hidden',
    marginBottom: 20,
    position: 'relative',
    height: 140,
    justifyContent: 'flex-end',
    borderWidth: 1,
    borderColor: '#6A2C91',
  },
  bannerImage: {
    ...StyleSheet.absoluteFillObject,
    width: '100%',
    height: '100%',
  },
  bannerText: {
    color: '#F3E5F5',
    fontSize: 13,
    fontStyle: 'italic',
    backgroundColor: 'rgba(45, 18, 72, 0.8)',
    padding: 8,
    textAlign: 'center',
  },
  sectionContainer: {
    marginBottom: 10,
  },
  sectionTitle: {
    fontSize: 16,
    fontWeight: 'bold',
    color: '#E8D7F1',
    marginBottom: 10,
  },
  entryCard: {
    backgroundColor: '#431C6B',
    borderRadius: 8,
    padding: 12,
    marginBottom: 10,
    borderLeftWidth: 4,
    borderLeftColor: '#BA68C8', // Detalhe lateral em lilás
    borderWidth: 1,
    borderColor: '#6A2C91',
  },
  entryHeader: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    marginBottom: 6,
  },
  entryTitle: {
    fontSize: 14,
    fontWeight: 'bold',
    color: '#FFFFFF',
  },
  entryDate: {
    fontSize: 11,
    color: '#C9A8E8',
  },
  entryDesc: {
    fontSize: 13,
    color: '#E8D7F1',
  },
  footer: {
    padding: 10,
    backgroundColor: '#431C6B',
    alignItems: 'center',
    borderTopWidth: 1,
    borderTopColor: '#6A2C91',
  },
  footerText: {
    fontSize: 10,
    color: '#C9A8E8',
  },
});
